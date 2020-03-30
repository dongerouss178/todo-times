<template>
  <v-app :dark="isDark">
    <v-app-bar
      app
      color="primary"
      dark
    >
    <v-toolbar-side-icon></v-toolbar-side-icon>
      <v-toolbar-title class="headline">My Todo</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <TodoList></TodoList>
    </v-content>
  </v-app>
</template>

<script>
import TodoList from './components/TodoList';

export default {
  name: 'App',

  components: {
    TodoList,
  },

  data: () => ({
    //
  }),
};
</script>
3