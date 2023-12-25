<template>
  <div :class="message.type === 'user' ? 'user-message' : 'bot-message'">
    {{ message.text }}
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.user-message {
  margin-left: auto;
  width: fit-content;
  max-width: 75%;
  background-color: #007aff;
  color: #ffffff;
  font-size: 14px;
  padding: 0.6em;
  border-radius: 10px 0 10px 10px;
  box-shadow: 1px 1px 2px 0 #0a0937;
}

.bot-message {
  margin: 10px 0;
  background-color: #f2f2f7;
  width: fit-content;
  max-width: 65%;
  font-size: 14px;
  padding: 0.6em;
  border-radius: 0 15px 15px 15px;
  box-shadow: 1px 1px 2px 0 #0a0937;
}
</style>
