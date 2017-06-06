<template>
  <router-view></router-view>
</template>

<script>
  define(["Vue", "vue-head"], function(Vue, VueHead) {
    Vue.use(VueHead);
    return Vue.component("default-component", {
      template: template, // the variable template will be injected
      data: function() {
        return {
          meta: {
            meta_title: null,
            meta_description: null,
            meta_keywords: null
          }
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
      head: {
        title: function () {
          return {
            title: this.meta.meta_title
          }
        },
        meta: function () {
          return {
            meta: [
              {name: 'description', content: this.meta.meta_description},
              {name: 'keywords', content: this.meta.meta_keywords}
            ]
          }
        }
      }
    });
  });
</script>