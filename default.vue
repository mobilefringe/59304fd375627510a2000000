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
          meta: {}
        }
      },
      beforeRouteEnter (to, from, next) {
        next(vm => {
          // access to component instance via `vm`
          vm.meta = vm.findMetaByPath(to.path);
        })
      },
      beforeRouteUpdate (to, from, next) {
        this.meta = this.findMetaByPath(to.path);
      },
      computed: {
        findMetaByPath () {
          return this.$store.getters.findMetaByPath;
        }
      },
      metaInfo () {
        return {
          title: this.meta.meta_title,
          meta: [
            {name: 'description', content: this.meta.meta_description}
          ]
        }
      }
    });
  });
</script>