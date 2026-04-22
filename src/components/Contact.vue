 <template>
   <section id="contact">
     <div class="contact-wrapper">
       <h2>Contact Me</h2>

       <form class="contact-form" @submit.prevent="submitForm">

         <div class="contact-group">
           <label class="contact-label">Name</label>
           <input
             v-model="form.name"
             type="text"
             class="contact-input"
             placeholder="John Doe"
           />
         </div>

         <div class="contact-group">
           <label class="contact-label">Email</label>
           <input
             v-model="form.email"
             type="email"
             class="contact-input"
             placeholder="john@mail.com"
           />
         </div>

         <div class="contact-group">
           <label class="contact-label">Message</label>
           <textarea
             v-model="form.message"
             rows="5"
             class="contact-textarea"
             placeholder="Write your message..."
           ></textarea>
         </div>

         <!-- reCAPTCHA -->
         <div
           class="g-recaptcha"
           data-sitekey="6LdxLL8sAAAAAJGUd1kc6cCAXceU3z4C58w7zxzs"
           data-callback="onRecaptchaSuccess"
         ></div>

         <button
           type="submit"
           class="contact-submit-btn"
           :disabled="loading"
         >
           {{ loading ? "Sending..." : "Submit" }}
         </button>

       </form>
     </div>
   </section>
 </template>

 <script>
 import emailjs from "@emailjs/browser"

 export default {
   data() {
     return {
       loading: false,
       recaptchaToken: "",
       form: {
         name: "",
         email: "",
         message: ""
       }
     }
   },

   mounted() {
     window.onRecaptchaSuccess = (token) => {
       this.recaptchaToken = token
     }

     window.onRecaptchaExpired = () => {
       this.recaptchaToken = ""
     }
   },

   methods: {
     async submitForm() {
       if (!this.form.name || !this.form.email || !this.form.message) {
         alert("Please fill out all fields.")
         return
       }

       const isLocal = window.location.hostname === "localhost"

       if (!this.recaptchaToken && !isLocal) {
         alert("Please verify reCAPTCHA")
         return
       }

       this.loading = true

       try {
         await emailjs.send(
           "service_jaexwwi",
           "template_az84qfo",
           {
             from_name: this.form.name,
             from_email: this.form.email,
             message: this.form.message
           },
           "eoVdagvx62_wzPa8g"
         )

         alert("Message sent successfully!")

         this.form.name = ""
         this.form.email = ""
         this.form.message = ""

         this.recaptchaToken = ""

         if (window.grecaptcha) {
           window.grecaptcha.reset()
         }

       } catch (err) {
         console.log(err)
         alert("Failed to send message.")
       }

       this.loading = false
     }
   }
 }
 </script>