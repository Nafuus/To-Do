<template>
  <v-app>
    <todo />
  </v-app>
</template>

<script>
import todo from './components/todo.vue'

export default {
  name: 'App',
  components: {
    todo
  },
  data () {
    return {

    }
  }
}
</script>
