<template>
  <div class="messagebox">
  <div class="row message" :class="{ read: hasRead, unread: !hasRead, selected: selected, unselected: !selected}">
  <div class="col-xs-1">
    <div class="row">
      <div class="col-xs-2">
        <input @click="toggleSelected" class="checkbox" type="checkbox" v-model="checked"/>
      </div>
      <div class="col-xs-2">
         <a v-on:click="unstarMessage"><icon v-if="stars" class="star" name="star"></icon></a>
         <a v-on:click="starMessage"><icon v-if="!stars" class="star" name="star-o"></icon></a>
      </div>
    </div>
  </div>
  <div class="col-xs-11">
    <a href="#">
      <b-badge class="label" variant="warning" v-for="label in labels" key="">{{ label }}</b-badge>
      {{ email.subject }}
    </a>
  </div>
</div>
</div>
</template>


<script>
  export default {
  name: 'email',
  props: ['email'],
  data () {
    return {
      starred: 'star-o',
      hasRead: this.email.read,
      selected: this.email.selected,
      checked: this.email.selected,
      stars: this.email.starred,
      labels: this.email.labels
    }
  },
  methods: {
    starMessage(event) {
      this.stars = true;
    },
    unstarMessage(event) {
      this.stars = false;
    },
    toggleSelected(event) {
      if (this.selected === true) {
        this.selected = false
      } else {
        this.selected = true
      }
    }
  },
  mounted() {

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
