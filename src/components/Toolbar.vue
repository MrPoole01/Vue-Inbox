<template>
  <div class="row toolbar">
  <div class="col-md-12">
    <p class="pull-right">
      <b-span name="badge badge">2</b-span>
      unread messages
    </p>

    <b-button class="btn btn-default">
      <icon name="check-square-o"></icon>
    </b-button>

    <b-button class="btn btn-default">
      Mark As Read
    </b-button>

    <b-button class="btn btn-default">
      Mark As Unread
    </b-button>

    <select class="form-control label-select">
      <option value="Apply label">Apply label</option>
      <option value="dev">dev</option>
      <option value="personal">personal</option>
      <option value="gschool">gschool</option>
    </select>

    <select class="form-control label-select">
      <option>Remove label</option>
      <option value="dev">dev</option>
      <option value="personal">personal</option>
      <option value="gschool">gschool</option>
    </select>

    <b-button class="btn btn-default">
      <icon name="trash-o"></icon>
    </b-button>
  </div>
</div>
</template>

<script>
export default {
      props: {
     options: {

    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.message {
  margin-left: 0px;
  padding-top: 8px;
  padding-bottom: 8px;
  cursor: pointer;
  border-bottom: 1px solid #efefef;
}

.message a {
  color: black;
}

.message a:hover, .message a:active, .message a:focus {
  text-decoration: none;
}

.message + .message {
  border-top: 1px solid #efefef;
}

.message.read {
  background: #efefef;
}

.message.unread {
  font-weight: bold;
}

.message.selected {
  background: #ffffcc;
}

.message:hover {
  margin-left: -3px;
  border-left: 3px solid #ccc;
}

.message-body {
  background: #ccc;
  margin-left: 0;
  margin-bottom: 1em;
  padding-top: 1em;
  padding-bottom: 1em;
}

.toolbar {
  margin-top: 1em;
  margin-bottom: 1em;
}

.toolbar .label-select {
  width: auto;
  display: inline;
}

.toolbar select,
.toolbar button,
.toolbar a,
.toolbar .badge {
  margin-right: .5em;
  margin-bottom: .5em;
}

footer.spacer {
  margin-bottom: 20em;
}

.label {
  margin-right: .5em;
}

.fa-close {
  cursor: pointer;
}
</style>
