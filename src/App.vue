<template>
  <div id="app">
    <h1>Formulario en Vue.js</h1>
    <FormularioVue @emit-form="addUser" />
    <InfoTabla :users="users" />
  </div>
</template>

<script>
import FormularioVue from "./components/FormularioVue.vue";
import InfoTabla from "./components/InfoTabla.vue";

export default {
  name: "App",
  components: {
    FormularioVue,
    InfoTabla,
  },
  data() {
    return {
      users: [],
    };
  },
  methods: {
    addUser(user) {
      this.users.push(user);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
