<template>
  <div class='alert'>
    <p class="alert_message">{{message}}</p> 
    <button class="alert_button" @click='closeAlert'><i class="fas fa-times"></i></button>
  </div>
</template>

<script>
export default {
  props:{
   message: String
  },
  methods:{
    closeAlert(){
      this.$emit('closeAlert')
    }
  }
};
</script>

<style lang="scss">
  .alert{
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 410px;
    height: 100px;
    background-color: rgb(211,211,211);
    border-radius: 20px;
    &_message{
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    &_button{
      position: absolute;
      font-size: 1rem;
      right: 0;
      border: none;
      padding: 10px;
      background-color: transparent;
      &:hover{
        cursor: pointer;
      }
    }
  }
</style>
