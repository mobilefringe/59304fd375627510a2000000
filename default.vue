<template>
  <router-view></router-view>
</template>

<script>
  define(["Vue", "vue-meta"], function(Vue, Meta) {
    Vue.use(Meta);
    return Vue.component("default-component", {
      template: template, // the variable template will be injected
      data: function() {
        return {
          meta: null
        }
      }
      computed: {
        findMetaDataByPath () {
          return this.$store.getters.findMetaDataByPath;
        }
      }
    });
  });
</script>