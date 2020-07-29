<template>
  <div id="app">
    <div v-for="(item) in menus" :key="item.key">
      <router-link  >{{item.title}}</router-link>
    </div>
    <router-view />
  </div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      menus: [
        {
          key: "vue",
          route: "/",
          title: "主页"
        }
        // {
        //   key: "vue-list",
        //   route: "/list",
        //   title: "列表页"
        // }
      ]
    };
  },

  computed: {
    currentRoute() {
      const menu = this.menus.find(item => item.route === this.$route.path);
      return menu ? menu.key : "vue";
    }
  }
};
</script>
