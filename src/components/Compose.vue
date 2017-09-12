<template>
  <b-form class="form-horizontal well" v-show="form">
  <div class="form-group">
    <div class="col-sm-8 col-sm-offset-2">
      <h4>Compose Message</h4>
    </div>
  </div>
  <div class="form-group">
    <label for="subject" class="col-sm-2 control-label">Subject</label>
    <div class="col-sm-8">
      <b-form-input type="text" class="form-control" id="subject" v-model="composeEmail.subject" placeholder="Enter a subject" name="subject"></b-form-input>
    </div>
  </div>
  <div class="form-group">
    <label for="body" class="col-sm-2 control-label">Body</label>
    <div class="col-sm-8">
      <textarea name="body" id="body" v-model="composeEmail.message" class="form-control"></textarea>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-8 col-sm-offset-2">
      <b-button @click="compose" type="submit" variant="primary">Send</b-button>
      <b-button @click="exitForm" type="submit" variant="primary">Cancel</b-button>
    </div>
  </div>
</b-form>
</template>

<script>
export default {
  name: 'form-horizontal',
  props: [
    'form',
    'inputForm',
    'exitForm',
    'composeEmail',
    'compose'
  ]
}
</script>
