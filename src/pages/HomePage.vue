<template>
  <div>
    <Navbar />
    <About />
    <Projects />
    <Tools />
    <Contact />
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue"
import About from "../components/About.vue"
import Projects from "../components/Projects.vue"
import Tools from "../components/Tools.vue"
import Contact from "../components/Contact.vue"

export default {
  components: {
    Navbar,
    About,
    Projects,
    Tools,
    Contact
  }
}
</script>