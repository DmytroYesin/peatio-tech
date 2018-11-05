<template>
  <div class="cta-sub no-color">
    <div class="container">
      <div class="cta-inner">
        <div v-if="show">
          <h1>Start your Peatio Cloud</h1>
          <p>Get in touch with our specialists.</p>
          <div class="form">
            <form id="signup" class="formee clearfix" action="#" novalidate="novalidate">
        ￼     <div class="form-name">
                <input v-model="company_name" name="company_name" id="company_name" type="text" placeholder="Your Company name" style="display: block; width: 100%">
              </div>
              <div >
                <input v-model="email" name="email" id="email" type="text" placeholder="Your Email" style="display: block; width: 100%">
              </div>
        ￼      <div class="form-button software">
                <button v-on:click.prevent="postPost()" class="btn btn-primary btn-action page-scroll mt-3 btn-block" data-wow-delay="0.2s" type="submit" title="Send">Contact Us</button>
              </div>
              <div v-if="incorrect > 0" class="alert alert-danger error-message" role="alert">
                Incorrect company name or email address
              </div>
            </form>
          </div>
        </div>
        <div v-else>
          <h1>
            <span class="big-text">
              Thank you!
            </span><br/>
            <span class="small-text">
              We will contact you ASAP!
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
        company_name: '',
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
          company_name: this.company_name
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
