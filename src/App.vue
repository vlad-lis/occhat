<template>
  <div id="app">
    <ChatWidget />
  </div>
</template>

<script>
import ChatWidget from './components/ChatWidget.vue'

export default {
  components: {
    ChatWidget
  }
}
</script>

<style>
#app {
  max-width: 350px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Arial', 'Verdana', sans-serif;
  font-weight: normal;
}
</style>
