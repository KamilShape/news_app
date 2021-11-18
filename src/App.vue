<template>
  <div class="newsApp">
    <h1 class="newsApp_header">NEWS</h1>
    <div class='newsApp_date'>{{dayOfTheWeek}} {{day}}/{{month}}/{{year}} </div>
    <input type="text" class="newsApp_search" v-model='searchingWord' placeholder="Search..."> 
    <button class="newsApp_button" @click='fetchData'><i class="fas fa-search"></i><p>Search...</p></button>
  </div>
  <Article
    v-for='article in articles'
    :key='article.url'
    :image='article.urlToImage'
    :title='article.title'
    :description='article.description'
    :url='article.url'
  />
</template>

<script>

import Article from '@/components/Article.vue'
export default {
  name: "App",
  data(){
    return{
      date: new Date,
      weekdays: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
      searchingWord: '',
      api_key: '9eb4691f409548d7b84d8d1b67ff7c65',
      url_key: 'https://newsapi.org/v2/everything?',
      articles: []
    }
  },
  components:{
    Article
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
    }
  },
  methods:{
    async fetchData(){
      this.articles = []
          try {
            let {data} = await this.axios(`${this.url_key}q=${this.searchingWord}&from=${this.year-this.month-this.day}&sortBy=publishedAt&apiKey=${this.api_key}`);
              data.articles.forEach(element => {
              this.articles.push(element);
            });
            console.log(this.articles)
          }
          catch(e) {
            console.log(e, 'Error')
          }
          this.searchingWord = ''
        }
  }
};

</script>

<style lang="scss">
.newsApp{
  width: 400px;
  margin: 30px auto;
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  padding: 30px; 
  border-radius: 20px;
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
    width: 100px;
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
  &_article{
    border: 1px solid black;
    padding: 20px;
  }
}
</style>
