<template>
  <div class="add uk-container">
    <form v-on:submit.prevent="onSubmit">
      <fieldset class="uk-fieldset">
          <legend class="uk-legend">Add Face to blockchain</legend>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Name" id="name" v-model="form.name">
          </div>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Face url (facebook/linkedin)" id="url" v-model="form.url">
          </div>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Face photo url" id="photo" v-model="form.photo">
          </div>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Face role" id="role" v-model="form.role">
          </div>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Project" id="project" v-model="form.project">
          </div>
          <div class="uk-margin">
              <input class="uk-input" type="text" placeholder="Project url" id="project_url" v-model="form.project_url">
          </div>
          <div class="uk-margin">
            <button class="uk-button uk-button-primary"><span uk-icon="icon: bolt"></span> Add</button>
          </div>
      </fieldset>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import UIkit from 'uikit/dist/js/uikit.min'
export default {
  name: 'add',
  data: () => ({
    form: {
      name: '',
      url: '',
      photo: '',
      role: '',
      project: '',
      project_url: ''
    }
  }),
  methods: {
    onSubmit: function () {
      // axios.post('/save', JSON.stringify(this.form))
      axios.post({
        url: '/save',
        data: JSON.stringify(this.form),
        headers: {'Content-Type': 'application/json'},
      })
      .then(response => {
        console.log(response.status)
        UIkit.notification('Face added')
      })
      .catch(e => {
        UIkit.notification('Error')
        this.errors.push(e)
      })
    }
  }
}
</script>
