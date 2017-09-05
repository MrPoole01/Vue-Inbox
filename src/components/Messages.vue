<template>
  <div class="messages">
    <Message
      v-for="email in emails"
      :email="email"
      :starMessage="starMessage"
      key="">
    </Message>
  </div>
</template>

<script>
import Message from "./Message"

export default {
  name: 'messages',
  props: [
    'emails',
    'starMessage'
  ],
  components: {
    Message
  }
}
</script>

<style>

</style>
