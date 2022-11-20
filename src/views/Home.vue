<template>
  <div v-if="projects.length">
    <FilterNav @filter-change="current = $event" :current="current" />
    <div v-for="project in filteredProjects" :key="project">
      <SingleProject  :project="project" @delete="handledelete" @complete="handlecomplete" /> 
    </div>
  </div>
</template>
<script>
import SingleProject from '@/components/SingleProject.vue'
import FilterNav from '@/components/FilterNav.vue'
export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(response => response.json())
      .then(data => this.projects = data)
      .catch(err => console.error(err.message))
  },
  methods: {
    handledelete(id) {
      this.projects = this.projects.filter(p => p.id !== id)
    },
    handlecomplete(id) {
      let p = this.projects.find(project => project.id === id);
      p.completed = !p.completed
    }
  },
  computed: {
    filteredProjects() {
      if(this.current === 'completed') {
        return this.projects.filter(project => project.completed)
      }
      if(this.current === 'ongoing') {
        return this.projects.filter(project => !project.completed)
      }
      return this.projects;
    }
  },
}
</script>
