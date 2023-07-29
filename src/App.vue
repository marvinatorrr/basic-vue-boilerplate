<template>
  <div id="app">
    <div class="nav">
      <b-button @click="openNewWindow">Click me for a pop up!</b-button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    async openNewWindow() {
      console.log("button is clicked!");
      const newWindow = window.open("", "_blank", "width=400,height=300");

      const bootstrapCSS = newWindow.document.createElement("link");
      bootstrapCSS.rel = "stylesheet";
      bootstrapCSS.href =
        "https://cdn.jsdelivr.net/npm/bootstrap@4.0/dist/css/bootstrap.min.css";
      newWindow.document.head.appendChild(bootstrapCSS);

      const bootstrapVueCSS = newWindow.document.createElement("link");
      bootstrapVueCSS.rel = "stylesheet";
      bootstrapVueCSS.href =
        "https://cdn.jsdelivr.net/npm/bootstrap-vue@2.0/dist/bootstrap-vue.css";
      newWindow.document.head.appendChild(bootstrapVueCSS);

      const appContainer = newWindow.document.createElement("div");
      newWindow.document.body.appendChild(appContainer);

      const [
        { default: Vue },
        { default: Popup },
        { default: BootstrapVue },
      ] = await Promise.all([
        import("vue"),
        import("./components/Popup.vue"),
        import("bootstrap-vue"),
      ]);

      Vue.use(BootstrapVue);

      new Vue({
        el: appContainer,
        render: (h) => h(Popup),
      });
    },
  },
};
</script>
