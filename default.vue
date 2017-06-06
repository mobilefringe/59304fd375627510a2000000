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
      },
      beforeRouteEnter (to, from, next) {
        next(vm => {
          // access to component instance via `vm`
          vm.meta = vm.findMetaDataByPath(to.path);
        })
      },
      beforeRouteUpdate (to, from, next) {
        this.meta = this.findMetaDataByPath(to.path);
        next();
      },
      computed: {
        findMetaDataByPath () {
          return this.$store.getters.findMetaDataByPath;
        }
      },
      
    });
  });
</script>