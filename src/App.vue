<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>TO DO APP</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        text
        href="http://datnt95.netlify.com/"
        target="_blank"
      >
        <span class="mr-2">DATNT76</span>
      </v-btn>
    </v-app-bar>
    <v-content class="custom_content" >
      <Todos/>
    </v-content>
  </v-app>
</template>

<script>
import Todos from './components/Todos.vue';

export default {
  name: 'App',
  components: {
    Todos,
  },
  data: () => ({
    //
  }),
};
</script>

<style >
  .custom_content{
    background-color: #0099ff;
  }
</style>
