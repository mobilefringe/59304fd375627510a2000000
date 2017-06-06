<template>
  <router-view></router-view>
</template>

<script>
  define(["Vue"], function(Vue) {
    return Vue.component("default-component", {
      template: template, // the variable template will be injected
        
      beforeRouteEnter (to, from, next) {
        next(vm => {
          // access to component instance via `vm`
          console.log(to);
        })
      },
      beforeRouteUpdate (to, from, next) {
        console.log(to);
      },
      computed: {
        findMetaByPath () {
          return this.$store.getters.findMetaByPath;
        }
      }        
    });
  });
</script>