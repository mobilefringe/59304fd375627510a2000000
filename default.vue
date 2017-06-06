<template>
  <router-view></router-view>
</template>

<script>
  define(["Vue"], function(Vue) {
    return Vue.component("default-component", {
      template: template, // the variable template will be injected
      data: function() {
        return {
          metaInfo: null
        }
      },
      beforeRouteEnter (to, from, next) {
        next(vm => {
          // access to component instance via `vm`
          vm.metaInfo = vm.findMetaByPath(to.path);
        })
      },
      beforeRouteUpdate (to, from, next) {
        this.metaInfo = this.findMetaByPath(to.path);
      },
      computed: {
        findMetaByPath () {
          return this.$store.getters.findMetaByPath;
        }
      }        
    });
  });
</script>