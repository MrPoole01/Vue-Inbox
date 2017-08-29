<template>
  <div class="messages">
    <Message v-for="email in emailList" :email="email" key=""></Message>
  </div>
</template>

<script>
import Message from "./Message"
import Data from "../Data/seeds"


export default {
  name: 'messages',
  components: {
    Message
  },
  data() {
    return {
      emailList: Data
    }
  }
}
</script>

<style>

</style>
