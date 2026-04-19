<template>
  <div>

    <!-- Navbar -->
    <nav class="navbar">
      <div class="nav-container">

        <a href="#landing" class="nav-logo">Ralph Tago</a>

        <ul class="nav-links" :class="{ active: isMenuOpen }">
          <li><a href="#landing">Home</a></li>
          <li><a href="#projects">Projects</a></li>
          <li><a href="#tools">Tools</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>

        <div class="nav-toggle" @click="toggleMenu">
          &#9776;
        </div>

      </div>
    </nav>

    <!-- Landing -->
    <section id="landing">
      <div class="landing-wrapper">
        <h1>Ralph Tago</h1>
        <h2>Full Stack Web Developer</h2>
        <p>Welcome to my portfolio. Explore my projects, tools I use, and get in touch!</p>
      </div>
    </section>

    <!-- Projects -->
    <section id="projects">
      <div class="projects-wrapper">
        <h2>My Projects</h2>
        <p>Here are some of my current and future projects:</p>

        <div class="projects-grid">
          <div
            class="project-card"
            v-for="project in projects"
            :key="project.title"
          >
            <img :src="project.image" class="project-image" />
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <p v-if="project.extra">{{ project.extra }}</p>
          </div>
        </div>

      </div>
    </section>

    <!-- Tools -->
    <section id="tools">
      <div class="tools-wrapper">
        <h2>Tools I Use</h2>
        <p>Here are some of the tools and technologies I work with:</p>

        <ul class="tools-list">
          <li>HTML5</li>
          <li>CSS3 / Sass</li>
          <li>JavaScript / ES6</li>
          <li>Bootstrap</li>
          <li>Figma</li>
          <li>Git / GitHub</li>
        </ul>
      </div>
    </section>

    <!-- Contact -->
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
              placeholder="john.doe@mail.com"
            />
          </div>

          <div class="contact-group">
            <label class="contact-label">Message</label>
            <textarea
              v-model="form.message"
              class="contact-textarea"
              rows="5"
              placeholder="Write your message here..."
            ></textarea>
          </div>

          <button type="submit" class="contact-submit-btn" :disabled="loading">
            {{ loading ? "Sending..." : "Submit" }}
          </button>

        </form>
      </div>
    </section>

  </div>
</template>

<script>
import projectsData from '../data/projects.json'
import emailjs from '@emailjs/browser'

export default {
  name: "HomePage",

  data() {
    return {
      projects: projectsData,
      isMenuOpen: false,
      loading: false,

      form: {
        name: "",
        email: "",
        message: ""
      }
    }
  },

  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },

    async submitForm() {
      if (!this.form.name || !this.form.email || !this.form.message) {
        alert("Please fill out all fields.")
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

      } catch (error) {
        console.log("EmailJS Error:", error)
        alert("Failed to send message. Please try again.")
      }

      this.loading = false
    }
  }
}
</script>