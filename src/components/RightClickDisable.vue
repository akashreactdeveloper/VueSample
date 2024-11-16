<template>
    <div>
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    mounted() {
      document.addEventListener("contextmenu", this.disableRightClick);
    },
    beforeDestroy() {
      document.removeEventListener("contextmenu", this.disableRightClick);
    },
    methods: {
      disableRightClick(event) {
        event.preventDefault();
        console.log("Right-click disabled"); 
      }
    }
  };
  </script>
  
  <style scoped>
  </style>
  