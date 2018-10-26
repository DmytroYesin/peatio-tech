<template>
  <div class="cta-sub no-color">
    <div class="container">
      <div class="cta-inner">
        <div>
          <h1>Start your Peatio Cloud</h1>
          <p>Please submit your email to receive your peatio.tech demo link.</p>
          <div class="form">
            <form id="signup" class="formee clearfix" action="#" novalidate="novalidate">
              <div v-if="incorrect > 0" class="alert alert-danger error-message alert-box" role="alert" style="width: 100%; margin-top: -10px;">
                <div class="alert-font text-center">
                  Incorrect url or email address
                </div>
              </div>
              <div v-if="!this.show" class="alert alert-success alert-box" style="width: 100%; margin-top: -10px;">
                <div class="success-font text-center">
                  Thank you for contacting us, <br/> we will be in touch shortly
                </div>
                <div class="small-text text-center">
                  Get in touch with our specialists
                </div>
              </div>
              <div v-if="incorrect < 1 && this.show" class="alert-box"></div>
        ￼     <div class="form-name subscribe-form">
                <div class="form-icon">
                  <i class="fas fa fa-link fa-1x"></i>
                </div>
                <div>
                  <input :disabled="!this.show" v-model="company_website" name="company_website" id="company_website" type="url" placeholder="Your Company Website" style="display: block; width: 100%; padding-left: 10px; padding-right: 50px; background-color: white;">
                </div>
              </div>
              <div class="form-name subscribe-form">
                <div class="form-icon">
                  <i class="fas fa fa-envelope fa-1x"></i>
                </div>
                <div>
                  <input :disabled="!this.show" v-model="email" name="email" id="email" type="text" placeholder="Your Company Email" style="display: block; width: 100%; padding-left: 10px; padding-right: 50px; background-color: white;">
                </div>
              </div>
        ￼     <div class="form-button">
                <button :disabled="!this.show" v-on:click.prevent="postPost()" class="right button" type="submit" title="Send">Submit</button>
              </div>
            </form>
          </div>
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
