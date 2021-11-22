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
  height: 200px;
  display: flex;
  padding: 10px;
  box-sizing: border-box;
  border: 1px solid black;
  border-radius: 30px;
  overflow: hidden;


    &_image{
      position: relative;
    }
    &_icon{
      font-size: 40px;
    }
    &_title_container{
      position: absolute;
      top: 50%;
      right: 0%;
      transform: translate(-12.5%,-50%);
      width: 150px;
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
@media (min-width: 768px) {
  .article{
    flex-direction: column;
    width: 250px;
    height: 350px;
      &_image{
        border-radius: 1px solid black;
      width: 200px;
        top: 25%;
        left: 50%;
        transform: translate(-50%);
    }
     &_title_container{
      top: 70%;
      right: 0%;
      width: 200px;
    }
  }
  img {
    width: 100%;
}
}
</style>
