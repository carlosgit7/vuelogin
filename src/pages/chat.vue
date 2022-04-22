<template>
     <h1 class="text-6xl font-thin tracking-tighter text-center mt-8">
    Cool Chat
  </h1>
  <div
    class="
      min-h-[500px]
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
          class="flex justify-between px-4 py-2 rounded-lg"
          :class="user === message.author ? 'bg-yellow-200' : 'bg-gray-200'"
        >
          <span>{{ message.text }}</span
          ><span>by {{ message.author }}</span>
        </div>
      </li>
    </ul>
    <div>
      <input
        class="w-full p-4 focus:outline-none focus:bg-yellow-200"
        type="text"
        placeholder="Type a message..."
        v-model="newMessage"
        @change="send"
      />
    </div>
  </div>
</template>