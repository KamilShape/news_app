<template>
  <div class="newsApp">
    <div class="newsApp_wrapper">
      <div class="newsApp_searchWindow">
        <h1 class="newsApp_header">NEWS</h1>
        <div class='newsApp_date'>{{dayOfTheWeek}} {{day}}/{{month}}/{{year}} </div>
        <input type="text" class="newsApp_search" v-model='searchingWord' placeholder="Search..."> 
        <button class="newsApp_button" @click='searchArticles'><i class="fas fa-search"></i><p>Search...</p></button>
      </div>
      <div class="newsApp_container">
        <Article
          v-for='article in articles'
          :key='article.url'
          :image='article.urlToImage'
          :title='article.title'
          :description='article.description'
          :url='article.url'
        />
      </div>
      <Alert
      :message='alertMessage'
      v-if='alertVisible'
      @closeAlert = 'closeAlert'
      />
      <h3 class="newsApp_arrows" v-if='arrowsVisible'>
        <button class="newsApp_button" @click='changePageToFirst'><i class="fas fa-angle-double-left"></i></button>
        <button class="newsApp_button" @click='changePageDown'><i class="fas fa-angle-left"></i></button>
        <p class="newsApp_pageCounter">{{currentPage}} / {{pages}}</p>
        <button class="newsApp_button" @click='changePageUp'><i class="fas fa-angle-right"></i></button>
        <button class="newsApp_button" @click='changePageToLast'><i class="fas fa-angle-double-right"></i></button>
      </h3>

    </div>
  </div>
</template>

<script>

import Alert from '@/components/Alert.vue'
import Article from '@/components/Article.vue'

export default {
  name: "App",
  data(){
    return{
      api_key: '9eb4691f409548d7b84d8d1b67ff7c65',
      url_key: 'https://newsapi.org/v2/everything?',
      articles: [],
      date: new Date,
      weekdays: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
      searchingWord: '',
      currentPage: 1,
      maxPerPage: 20,
      totalResults: 0,
      arrowsVisible: false,
      alertVisible: false,
      alertMessage: '', 
    }
  },
  components:{
    Article,
    Alert
  },
  computed:{
    dayOfTheWeek(){
      let day = this.date.getDay()
      return this.weekdays[day]
    },
    day(){
      return this.date.getDate()
    },
    month(){
      return this.date.getMonth() + 1
    },
    year(){
      return this.date.getFullYear() 
    },
    pages(){
      let numberOfPages = Math.ceil(this.totalResults/this.maxPerPage)
      if(numberOfPages <=5) {
       return numberOfPages
      } else {
        return 5
      }
    }
  },
  methods:{
    async fetchData(actualPage){
          this.arrowsVisible = false
          try {
            let {data} = await this.axios(`${this.url_key}q=${this.searchingWord}&from=${this.year}-${this.month}-${this.day}&pageSize=${this.maxPerPage}&page=${actualPage}&sortBy=publishedAt&apiKey=${this.api_key}`);
              this.totalResults = data.totalResults
              data.articles.forEach(element => {
              this.articles.push(element);
            });
          }
          catch(e) {
            console.log(e, 'Error')
          }
          if(this.totalResults > 0){
             this.arrowsVisible = true
          }
          else{
            this.alertMessage = 'No results :('
            this.alertVisible = true
          }
      },
      searchArticles(){
        if(this.searchingWord !== ''){
          this.articles = []
          this.currentPage = 1
          this.fetchData(this.currentPage)
        } else{
          this.alertMessage = 'Please fill searching word'
          this.alertVisible = true
        }
       },

      changePageUp(){
        if(this.currentPage < this.pages){ 
          this.currentPage++
          console.log(this.currentPage)
          this.articles = []
          this.fetchData(this.currentPage)
        }
      },

      changePageDown(){
         if(this.currentPage > 1) {
            this.currentPage--
            console.log(this.currentPage)
            this.articles = []
            this.fetchData(this.currentPage)
         }
      },

      changePageToFirst(){
         if(this.currentPage > 1){
            this.currentPage = 1
            console.log(this.currentPage)
            this.articles = []
            this.fetchData(this.currentPage)
         }
       },

      changePageToLast(){
          if(this.currentPage < 5 ){
            this.currentPage = 5
            console.log(this.currentPage)
            this.articles = []
            this.fetchData(this.currentPage)
          }
       },
      closeAlert(){
        this.alertVisible = false
      }
  }
};

</script>

<style lang="scss">

.newsApp{
  &_wrapper{
     width: 400px;
     margin: 30px auto;
  }
  &_searchWindow{
    display: flex;
    flex-direction: column;
    width: 100%;
    margin:  10px auto;
    border: 1px solid black;
    padding: 30px; 
    box-sizing: border-box;
    border-radius: 20px;
  }
  &_header{
    text-align: center;
  }
  &_date{
    text-align: center;
    padding: 10px;
  }
  &_search{
    padding: 10px;
    border-radius: 5px;
    outline: none;
    border: 1px solid black
  }
  &_button{
    display: flex;
    justify-content: space-evenly;
    background-color: rgb(211,211,211);
    margin: 10px auto;
    padding: 10px;
    border-radius: 10px 0;
    border: none;
    transition: 0.5s;

    &:hover{
      cursor: pointer;
      border-radius: 0 10px;
    }
  }
  &_container{
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    width: 100%;
  }
  &_article{
    border: 1px solid black;
    padding: 20px;
   
  }
  &_arrows{
    display: flex;
    width: 40%;
    margin: 30px auto;
  }
  &_pageCounter{
    line-height: 50px;
  }
  @media (min-width: 768px) {
    .newsApp{
      &_wrapper{
        width: 600px;
      }
      &_container {
        flex-direction: row;
        flex-wrap: wrap;
        }
      &_searchWindow{
        width: 500px;
        }
      &_arrows{
        width: 30%;
        }
      }
    }
  @media (min-width: 1024px) { 
    .newsApp{
      &_wrapper{
        width: 950px;
        }
      &_arrows{
        width: 20%;
        }
      }
    }
  @media (min-width: 1280px) {
    .newsApp{
      &_wrapper{
        width: 1100px;
        }
      }
    }
}
</style>
