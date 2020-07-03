<template>
  <div class="home">
    <HelloWorld msg="HelloWorld msg" />
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
<style lang="css" scoped>
.home{

  border:1px solid black;

}

</style>
