<template>
  <a :href='url' class="article" target="_blank">
    <div class="article_image"  >
      <img v-if='url' :src="image">
      <i v-else class="fas fa-images article_icon"></i>
      </div>
    <div class="article_title_container">
    <p class="article_title">{{title}}</p>
    </div>
  </a>
</template>

<script>
export default {
  data() {
    return{
      
    }
  },
  props:{
    title: String,
    image: String,
    description: String,
    url: String
  }
};
</script>

<style lang="scss">
.article{
  position: relative;
  margin:  10px auto;
  width: 400px;
  height: 150px;
  display: flex;
  padding: 30px;
  border: 1px solid black;
  border-radius: 30px;
   overflow: hidden;
  

    &_image{
      position: relative;
      background-color: red;
    }
    &_icon{
      font-size: 40px;
    }
    &_title_container{
      position: absolute;
      top: 50%;
      right: 0%;
      transform: translateY(-50%);
      width: 200px;
      padding: 5px;
      
      
    }
    &_title{
      padding: 10px;
      color: black;
    }
}
img {
    position: absolute;
    max-width: 200px;
    max-height: 150px;
    height: auto;
    top: 50%;
    transform: translateY(-50%);
    border-radius: 20px;
}
img:hover{
    cursor: pointer;
}
</style>
