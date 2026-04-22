<template>
  <section id="projects">
    <div class="projects-wrapper">
      <h2>My Projects</h2>
      <p>Here are some of my current and future projects:</p>

      <div class="projects-grid">
        <ProjectCard
          v-for="project in projects"
          :key="project.title"
          :project="project"
        />
      </div>

    </div>
  </section>
</template>

<script>
import projectsData from "../data/projects.json"
import ProjectCard from "./ProjectCard.vue"

export default {
  components: { ProjectCard },

  data() {
    return {
      projects: projectsData
    }
  }
}
</script>