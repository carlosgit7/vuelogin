<script setup>
  import { onUnmounted, ref } from 'vue'
  import useChat from '../composables/useChat'
  import useAuth from '../composables/userAuth'
  const { messages, unsubscribe, sendMessage } = useChat()
  const { user } = useAuth()

  const newMessage = ref('')

  const send = () => {
    sendMessage(newMessage.value)
    newMessage.value = ''
  }

  onUnmounted(() => {
    unsubscribe()
  })
</script>

<template>
     <h1 class="text-6xl font-thin tracking-tighter text-center mt-8">
    Chat Room
  </h1>
  <div
    class="
      min-h-[400px]
      w-1/2
      mt-8
      rounded-lg
      shadow-2xl
      flex flex-col
      justify-between
    "
  >
    <ul class="p-4 space-y-4">
      <li v-for="message in messages" :key="message.id">
        <div
          class="flex justify-between px-4 py-2 rounded-lg italic"
          :class="user === message.author ? 'bg-orange-400' : 'bg-blue-400'"
        >
          <span>{{ message.text }}</span>
          <span class="not-italic">by {{ message.author }}</span>
        </div>
      </li>
    </ul>
    <div>
      <input
        class="w-full p-4 focus:outline-none bg-lime-200"
        type="text"
        placeholder="Type a message..."
        v-model="newMessage"
        @change="send"
      />
    </div>
  </div>
</template>