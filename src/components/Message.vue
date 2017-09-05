<template>
  <div class="messagebox">
  <div class="row message" :class="{read: email.read, unread: !email.read, selected: email.selected}">
  <div class="col-xs-1">
    <div class="row">
      <div class="col-xs-2">
        <input class="checkbox" type="checkbox" :class="email.selected" v-model="email.selected"/>
      </div>
      <div @click="starMessage(email)" class="col-xs-2">
         <icon v-if="email.starred" class="star" name="star"></icon>
         <icon v-if="!email.starred" name="star-o" class="star"></icon>
      </div>
    </div>
  </div>
  <div class="col-xs-11">
    <a href="#">
      <b-badge class="label" variant="warning" v-for="label in email.labels" key="">{{ label }}</b-badge>
      {{ email.subject }}
    </a>
  </div>
</div>
</div>
</template>


<script>

  export default {
  name: 'messagebox',
  props: [
    'email',
    'starMessage',
    'bulkSelect'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
