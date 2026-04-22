<template>
  <div class="project-card">
    <img :src="project.image" class="project-image" />
    <h3>{{ project.title }}</h3>
    <p>{{ project.description }}</p>
    <p v-if="project.extra">{{ project.extra }}</p>
  </div>
</template>

<script>
export default {
  props: {
    project: Object
  }
}
</script>