<template>
  <p class="pull-right">
    <b-badge class="badge" pill variant=""  name="badge">{{ counter }}</b-badge>
    unread messages
  </p>
</template>

<script>
import Data from "../Data/seeds"
// console.log(Data);

export default {
  name: 'badge',
  data() {
    return {
      readMessages: Data,
      counter: 0
    }
  },
  methods: {
      count() {
        this.readMessages.map((message) => {
          if (message.read === false) {
            this.counter++
          }
        })
      }
    },
    mounted() {
      this.count()
    },
  }

</script>

<style>

</style>
