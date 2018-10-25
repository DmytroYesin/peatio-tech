<template>
  <div class="cta-sub no-color">
    <div class="container">
      <div class="cta-inner">
        <div v-if="show">
          <h1>Start your Peatio Cloud</h1>
          <p>Please submit your email to receive your peatio.tech demo link.</p>
          <div class="form">
            <form id="signup" class="formee clearfix" action="#" novalidate="novalidate">
        ￼     <div class="form-name">
                <input :disabled="!this.show" v-model="company_website" name="company_website" id="company_website" type="url" placeholder="Your Company Website" style="display: block; width: 100%">
              </div>
              <div >
                <input :disabled="!this.show" v-model="email" name="email" id="email" type="text" placeholder="Your Company Email" style="display: block; width: 100%">
              </div>
        ￼      <div class="form-button">
                <button :disabled="!this.show" v-on:click.prevent="postPost()" class="right button" type="submit" title="Send">Submit</button>
              </div>
              <div v-if="incorrect > 0" class="alert alert-danger error-message" role="alert">
                Incorrect url or email address
              </div>
            </form>
          </div>
        </div>
        <div v-else>
          <h1>
            <span class="big-text">
              Thank you for contacting us, we will be in touch shortly
            </span><br/>
            <span class="small-text">
              Get in touch with our specialists
            </span>
          </h1>
        </div>
        <div id="response"></div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data () {
      return {
        email: '',
        company_website: '',
        show: true,
        incorrect: 0,
        errors: []
      }
    },
    // Pushes posts to the server when called.
    methods: {
      postPost () {
        window.ga('send', {
          hitType: 'event',
          eventCategory: 'contact',
          eventAction: 'click',
          eventLabel: ''
        })
        axios.post(`/subscribers`, {
          email: this.email,
          company_website: this.company_website
        })
        .then(response => {
          this.show = false
        })
        .catch(e => {
          this.incorrect += 1
          this.errors.push(e)
        })
      }
    }
  }
</script>
