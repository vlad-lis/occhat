<template>
  <div class="chatbox" ref="chatbox">
    <div v-if="greetingMessage">
      <Message :message="greetingMessage" />
      <div class="option" v-for="option in options" :key="option.id" @click="selectOption(option)">
        {{ option.label }}
      </div>
    </div>
    <div v-for="message in messages" :key="message.id">
      <Message :message="message" />
    </div>
    <div class="user-input">
      <input
        class="input-field"
        v-model="userInput"
        @keyup.enter="sendMessageFromInput"
        placeholder="Введите сообщение..."
      />
      <button class="send-btn" @click="sendMessageFromInput">></button>
    </div>
  </div>
</template>

<script>
import Message from './MessageItem.vue'

export default {
  data() {
    return {
      userInput: '',
      messages: [],
      options: [
        { id: 1, label: 'Заказать пиццу' },
        { id: 2, label: 'Установить будильник' },
        { id: 3, label: 'Вывести погоду' }
      ],
      greetingMessage: null
    }
  },
  mounted() {
    this.showGreeting()
  },
  methods: {
    showGreeting() {
      this.greetingMessage = {
        id: this.messages.length + 1,
        text: 'Привет! Что я могу для Вас сделать?',
        type: 'bot'
      }
    },
    sendMessage(responseText) {
      const userMessage = {
        id: this.messages.length + 1,
        text: this.userInput,
        type: 'user'
      }
      this.messages.push(userMessage)
      this.userInput = ''

      const botResponse = {
        id: this.messages.length + 1,
        text: responseText,
        type: 'bot'
      }
      this.messages.push(botResponse)

      this.$nextTick(() => {
        this.$refs.chatbox.scrollTop = this.$refs.chatbox.scrollHeight
      })
    },
    sendMessageFromInput() {
      if (this.userInput.trim() !== '') {
        const matchedOption = this.options.find(
          (option) => option.label.toLowerCase() === this.userInput.toLowerCase()
        )
        if (matchedOption) {
          this.selectOption(matchedOption)
        } else {
          this.sendMessage('Неизвестная команда. Попробуйте еще раз.')
        }
      }
    },
    selectOption(option) {
      this.userInput = option.label
      switch (option.id) {
        case 1:
          this.sendMessage('Хорошо, я закажу пиццу. Что еще могу сделать?')
          break
        case 2:
          this.sendMessage('Хорошо, я установлю будильник. Что еще могу сделать?')
          break
        case 3:
          this.sendMessage('Хорошо, я выведу погоду. Что еще могу сделать?')
          break
        default:
          this.sendMessage('Неизвестный запрос')
          break
      }
    }
  },
  components: {
    Message
  }
}
</script>

<style scoped>
.chatbox {
  display: flex;
  flex-direction: column;
  height: calc(440px);
  padding: 7px 15px;
  overflow-y: scroll;
  border-radius: 3%;
  border: 1px solid black;
  box-shadow: 0 0 2px 0 #0a0937;
}

.user-input {
  display: flex;
  margin-top: auto;
  padding: 7px 0;
}

.input-field {
  flex: 1;
  padding: 0.3em;
  font-size: 14px;
}

.input-field:focus {
  outline: none;
}

.send-btn {
  margin-left: 5px;
  padding: 0.3em 0.6em;
  font-size: 14px;
  cursor: pointer;
  border: 1px solid black;
  border-radius: 25%;
}

.send-btn:focus {
  outline: 1px solid black;
}

.option {
  background-color: #f4f4fb;
  padding: 0.4em;
  margin-bottom: 3px;
  width: fit-content;
  max-width: 65%;
  font-size: 14px;
  border-radius: 15px;
  box-shadow: 1px 1px 2px 0 #0a0937;
}

.option:hover {
  cursor: pointer;
  background-color: #e5e5e9;
}
</style>
