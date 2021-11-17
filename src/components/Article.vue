<template>
  <div class="newsApp">
 
  </div>
</template>

<script>


export default {
  name: "App",
  data(){
    return{
      date: new Date,
      weekdays: ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'],
      api_key: '9eb4691f409548d7b84d8d1b67ff7c65',
      url_key: 'https://newsapi.org/v2/everything?'
    }
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
};

</script>

<style lang="scss">
.newsApp{
  width: 300px;
  margin: 30px auto;
  display: flex;
  flex-direction: column;
  border: 1px solid black;
  padding: 30px; 

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
}
</style>
