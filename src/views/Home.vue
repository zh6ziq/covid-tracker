<template>
  <div class="home">
    
    <HelloWorld msg="COVID-19 STATISTICS" desc="Get statistics of all countries about Covid-19." desc1="Updated every 15 minutes." />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    HelloWorld
  }
};
</script>