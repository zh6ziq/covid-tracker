<template>
  <div class="hello">
    <div class="jumbotron bg-transparent">
      <div class="my-3">
        <h1 class="text-white">{{ msg }}</h1>
        <h5 class="text-white">{{ desc }}</h5>
        <h5 class="text-white">{{ desc1 }}</h5>
      </div>
      <div class="my-3">
        <b-button variant="info"><router-link to="/tracker">GET STATISTICS</router-link></b-button>
      </div>
      <img alt="World Map" src="../assets/worldmap.png" class="w-50 mt-4" />
    </div>
    
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    desc: String,
    desc1: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #ffffff;
  text-decoration: none!important;
}
a:hover{
  color: #ffffff;
}
.hello{
  margin: 100px auto;
}
</style>
