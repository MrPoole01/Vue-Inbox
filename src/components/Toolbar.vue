
<template>
  <div class="row toolbar">
    <div class="col-md-12">

      <b-button @click="inputForm" class="btn btn-danger">
        <icon name="plus"></icon>
      </b-button>

      <b-button class="btn btn-default" @click="bulkSelect">
        <icon v-if="halfCheckbox"  name="minus-square-o"></icon>
        <icon v-if="bulkCheckbox"  name="check-square-o"></icon>
        <icon v-if="emptyCheckbox" name="square-o"></icon>
      </b-button>

      <b-button @click="markRead" class="btn btn-default" :disabled="emptyCheckbox">Mark As Read</b-button>

      <b-button @click="markUnread"class="btn btn-default" :disabled="emptyCheckbox">Mark As Unread</b-button>

      <b-form-select
        v-model="selected"
        :options="options"
        :disabled="emptyCheckbox"
        class="form-control label-select">
        <div>Selected: <strong>{{ selected }}</strong></div>
      </b-form-select>

      <b-form-select
        v-model="unselected"
        :options="unoption"
        :disabled="emptyCheckbox"
        class="form-control label-select">
        <div>Selected2: <strong>{{ unselected }}</strong></div>
      </b-form-select>

      <b-button @click="deleteEmail" class="btn btn-default" :disabled="emptyCheckbox">
        <icon name="trash-o"></icon>
      </b-button>

      <p class="pull-right">
        <b-badge class="badge" pill variant=""  name="badge">{{ unreadCount }}</b-badge>
        unread messages
      </p>

    </div>
  </div>
</template>


<script>

export default {
  name: 'toolbar',
  props: [
    'emails',
    'unreadCount',
    'markRead',
    'markUnread',
    'bulkCheckbox',
    'halfCheckbox',
    'emptyCheckbox',
    'starMessage',
    'bulkSelect',
    'inputForm',
    'deleteEmail',
    'form'
],
  data() {
      return {
        selected: null,
        options: [
         { value: null, text: 'Apply label' },
         { value: 'dev', text: 'dev' },
         { value: 'personal', text: 'personal' },
         { value: 'gschool', text: 'gschool'}
       ],
        unselected: null,
        unoption: [
         { value: null, text: 'Remove label' },
         { value: 'dev', text: 'dev' },
         { value: 'personal', text: 'personal' },
         { value: 'gschool', text: 'gschool'}
       ]
     }
   },
   watch: {
     selected(label) {
       const id = []
       if (label != null) {
         for (let i = 0; i < this.emails.length; i++) {
           let hasLabel = this.emails[i].labels.some(el => el == label)
           if (this.emails[i].selected && !hasLabel) {
             this.emails[i].labels.push(label)
             id.push(this.emails[i].id)
           }
         }
       }
       const data = {
         "messageIds": id,
         "command": "addlabel",
         "label" : label
       }
       const settings = {
         method: 'PATCH',
         headers: {
           'content-type': 'application/json'
         },
         body: JSON.stringify(data)
       }
       fetch(`${baseURL}/messages`, settings)
       .then(response => {
         if (response.ok) {
           console.log(response);
         }
       })
     },
     unselected(label) {
       const id = []
       if (label != null) {
         for (let i = 0; i < this.emails.length; i++) {
           let hasLabel = this.emails[i].labels.some(el => el == label)
           if (hasLabel && this.emails[i].selected) {
             let index = this.emails[i].labels.indexOf(label)
             this.emails[i].labels.splice(index, 1)
             id.push(this.emails[i].id)
           }
         }
       }
       const data = {
         "messageIds": id,
         "command": "removeLabel",
         "label" : label
       }
       const settings = {
         method: 'PATCH',
         headers: {
           'content-type': 'application/json'
         },
         body: JSON.stringify(data)
       }
       fetch(`${baseURL}/messages`, settings)
       .then(response => {
         if (response.ok) {
           console.log(response);
         }
       })
     }
   }
  }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
</style>
