<template>
  <div class="row toolbar">
    <div class="col-md-12">

      <b-button class="btn btn-danger">
        <icon name="plus"></icon>
      </b-button>

      <b-button class="btn btn-default">
        <icon name="minus-square-o"></icon>
      </b-button>

      <b-button class="btn btn-default">Mark As Read</b-button>

      <b-button class="btn btn-default">Mark As Unread</b-button>

      <b-form-select v-model="selected" :options="options" class="form-control label-select">
        <div>Selected: <strong>{{ selected }}</strong></div>
      </b-form-select>

      <b-form-select v-model="unselected" :options="unoption" class="form-control label-select">
        <div>Selected2: <strong>{{ unselected }}</strong></div>
      </b-form-select>

      <b-button class="btn btn-default">
        <icon name="trash-o"></icon>
      </b-button>

      <Badge></Badge>
    </div>
  </div>
</template>

<script>
import Badge from './Badge'

export default {
  name: 'toolbar',

  components: {
    Badge
  },
  data() {
    return {
      selected: null,
      options: [
       { value: null, text: 'Apply label' },
       { value: 'dev', text: 'dev' },
       { value: 'personal', text: 'personal' },
       { value: 'gschool', text: 'gschool', disabled: true }
     ],
      unselected: null,
      unoption: [
       { value: null, text: 'Remove label' },
       { value: 'dev', text: 'dev' },
       { value: 'personal', text: 'personal' },
       { value: 'gschool', text: 'gschool', disabled: true }
     ],
    }
  },
  methods: {

  }
}



</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >

</style>
