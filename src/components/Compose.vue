<template>
  <b-form class="form-horizontal well">
  <div class="form-group">
    <div class="col-sm-8 col-sm-offset-2">
      <h4>Compose Message</h4>
    </div>
  </div>
  <div class="form-group">
    <label for="subject" class="col-sm-2 control-label">Subject</label>
    <div class="col-sm-8">
      <b-form-input type="text" class="form-control" id="subject" placeholder="Enter a subject" name="subject"></b-form-input>
    </div>
  </div>
  <div class="form-group">
    <label for="body" class="col-sm-2 control-label">Body</label>
    <div class="col-sm-8">
      <textarea name="body" id="body" class="form-control"></textarea>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-8 col-sm-offset-2">
      <b-button type="submit" variant="primary">Send</b-button>
    </div>
  </div>
</b-form>
</template>

<script>
export default {

}
</script>

<style lang="css">
</style>
