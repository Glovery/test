<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <my-bar></my-bar>
  </div>
</template>

<script>
// @ is an alias to /src
import MyBar from "@/components/MyBar";
export default {
  name: "Home",
  components: {
    MyBar
  },
  methods: {}
};
</script>
