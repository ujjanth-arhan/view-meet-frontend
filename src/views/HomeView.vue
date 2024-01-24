<script setup>
import { onMounted, onUpdated, ref } from 'vue'

const messages = ref([])
var draftMessage = ref('')
const cwrap = ref()
var isClose = false

var socket;
onMounted(() => {
  chatScrollBot()
  socket = new WebSocket('wss://socketsbay.com/wss/v2/1/demo/')
  console.log('Mounted')
  socket.onopen = () => {
    console.log("opened")
  }
  socket.onerror = () => {
    console.log("error")
  }
  socket.onclose = () => {
    console.log('close')
    isClose = true
  }
  socket.onmessage = (event) => {
    messages.value.push({ message: event.data })
  }
})

onUpdated(() => {
  chatScrollBot()
})

function chatScrollBot() {
  if (cwrap.value != null && cwrap.value != undefined) {
    cwrap.value.scrollTop = cwrap.value.scrollHeight
  }
}

function sendMessage() {
  socket.send(draftMessage.value)
  messages.value.push({ message: draftMessage.value })
  draftMessage.value = ''
  chatScrollBot()
}
</script>

<template>
  <div class="home">
    <div class="chat-container">
      <h6 class="chat-notification" v-show="isClose">Please Refresh The Page</h6>
      <div ref="cwrap" class="chat-wrapper">
        <div v-for="message in messages" class="chat-item">{{ message.message }}</div>
      </div>
      <div class="chat-interaction-container">
        <input v-model="draftMessage" type="text" class="chat-input" @keypress.enter="sendMessage">
        <button @click="sendMessage" class="rounded-circle chat-send">
          <svg xmlns="http://www.w3.org/2000/svg" width="1.2em" height="1.2em" fill="currentColor" class="bi bi-send" viewBox="0 0 16 16">
            <path d="M15.854.146a.5.5 0 0 1 .11.54l-5.819 14.547a.75.75 0 0 1-1.329.124l-3.178-4.995L.643 7.184a.75.75 0 0 1 .124-1.33L15.314.037a.5.5 0 0 1 .54.11ZM6.636 10.07l2.761 4.338L14.13 2.576zm6.787-8.201L1.591 6.602l4.339 2.76z"/>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<style>
.chat-item {
  overflow: auto;
  overflow-y: auto;
}

.chat-wrapper {
  overflow: auto;
  margin: 4vh 1vh 8vh 4vh;
  max-height: 82vh;
}

.chat-container {
  max-width: 70vw;
  min-height: 100vh;
  max-height: 70vh;
  margin: auto;
  border: solid;
  border-radius: 2rem;
  position: relative;

}

.chat-interaction-container {
  padding: 2vh 4vh;
  position: absolute;
  bottom: 0px;
  border-top: solid;
  width: 100%;
}

.chat-send {
  width: 2.4rem;
  height: 2.4rem;
  border: solid;
}

.chat-input {
  padding-left: 1vw !important;
  width: 90%;
  border-radius: 1rem;
  padding: 0.5vh;
  margin-right: 1rem;
}

.chat-notification {
  text-align: center;
}

@media (max-width: 1024px) {
  .chat-input {
    padding-left: 1vw !important;
    width: 70%;
    border-radius: 1rem;
    padding: 0.5vh;
    margin-right: 1rem;
  }
}
</style>