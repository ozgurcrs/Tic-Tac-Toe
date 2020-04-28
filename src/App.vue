<template>
    <div class="container">
      <div class="title">Tic Tac Toe </div>
      <Play />
    </div>
</template>


<script>
import Play from './components/Play'
export default {
  components:{
    Play,
  }
}
</script>

<style>
  .container{
     margin:20px auto;
  }
  .title{
    height:auto;
    font-size:64px;
    text-align: center;
    padding:20px;
    font-weight:bold;
    color:#003049;
  }
</style>