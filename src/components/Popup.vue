<template>
  <div>
    hi this is my pop up
    <b-button @click="onClick">click me!</b-button>
  </div>
</template>

<script>
export default {
  methods: {
    onClick() {
      console.log("hello world!");
    },
  },
};
</script>

<style></style>
