<template>
<div id="App">
  <todo-app></todo-app>
</div>

  <router-view/>
</template>
<script>
import TodoApp from '@/components/todoApp.vue'
export default {
  name:'App',
  components:{
    TodoApp
  }
}
</script>
