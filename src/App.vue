<template>
<div id="app">

  <Toolbar
    :emails="emails"
    :bulkCheckbox="bulkCheckbox"
    :halfCheckbox="halfCheckbox"
    :emptyCheckbox="emptyCheckbox"
    :inputForm="inputForm"
    :markRead="markRead"
    :markUnread="markUnread"
    :bulkSelect="bulkSelect"
    :unreadCount="unreadCount"
    :starMessage="starMessage"
    :deleteEmail="deleteEmail"
    :baseURL="baseURL">
  </Toolbar>

  <Compose
    :inputForm="inputForm"
    :exitForm="exitForm"
    :form="form"
    :composeEmail="composeEmail"
    :compose="compose">
  </Compose>

  <Messages :emails="emails" :starMessage="starMessage">
  </Messages>


</div>
</template>

<script>
import Toolbar from './components/Toolbar'
import Compose from './components/Compose'
import Messages from './components/Messages'
const baseURL = 'https://inbox-ui.herokuapp.com/api'



export default {
  name: 'app',
  components: {
    Toolbar,
    Compose,
    Messages
  },
  data() {
    return {
      emails: [],
      form: false,
      composeEmail: {
        subject: '',
        message: ''
      }
    }
  },
  async mounted() {
    const data = await fetch(`${baseURL}/messages`)
    const response = await data.json()
    this.emails = response._embedded.messages.map(message => {
      message.selected = false
      return message
    })
  },
  computed: {
    unreadCount() {
      return this.emails.reduce((acc, email) => {
        if (email.read == false) {
          acc++
        }
        return acc
      }, 0)
    },
    bulkCheckbox() {
      return this.emails.every(email => email.selected)
    },
    halfCheckbox() {
      return this.emails.some(email => email.selected) && !this.bulkCheckbox
    },
    emptyCheckbox() {
      return this.emails.every(email => !email.selected)
    }
  },
  methods: {
    starMessage(message) {
      message.starred = !message.starred
      const data = {
        "messageIds": [message.id],
        "command": "star",
        "star" : message.starred
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
    bulkSelect() {
      if (this.bulkCheckbox) {
        this.emails.forEach(email => this.$set(email, 'selected', false))
      } else {
        this.emails.forEach(email => this.$set(email, 'selected', true))
      }
    },
    inputForm() {
      this.form = true
    },
    exitForm() {
      this.form = false
    },
    markRead() {
      const id = []
      for (let i = 0; i < this.emails.length; i++) {
        if (this.emails[i].selected) {
          this.emails[i].read = true
          id.push(this.emails[i].id)
        }
      }
      const data = {
        "messageIds": id,
        "command": "read",
        "read" : true
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
    markUnread() {
      const id = []
      for (let i = 0; i < this.emails.length; i++) {
        if (this.emails[i].selected) {
          this.emails[i].read = false
          id.push(this.emails[i].id)
        }
      }
      const data = {
        "messageIds": id,
        "command": "read",
        "read" : false
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
    deleteEmail() {
      const id = []
      this.emails = this.emails.filter(email => {
      if (email.selected) {
        id.push(email.id)
      }
      return !email.selected
      })
      const data = {
        "messageIds": id,
        "command": "delete"
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
    compose() {
      const data = {
        "subject": this.composeEmail.subject,
        "body": this.composeEmail.message
      }
      const settings = {
        method: 'POST',
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

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin-left: 5em;
  color: #2c3e50;
  margin-top: 60px;
}

.pull-right {
  display: inline-block;
  margin-left: 10%;
}

.messagebox {
  margin-left: 2em;
}

.checkbox {
  margin-left: 1.5em;
  margin-right: 2em;
}

.star {
  margin-right: 2em;
}

.message {
  margin-left: 0px;
  padding-top: 8px;
  padding-bottom: 8px;
  cursor: pointer;
  border-bottom: 1px solid #efefef;
}

.row {
  margin-right: -15px;
}

.message a {
  color: black;
}

.message a:hover,
.message a:active,
.message a:focus {
  text-decoration: none;
}

.message+.message {
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
  margin-left: 1em;
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

.form-horizontal {
  margin-left: 1em;
}
</style>
