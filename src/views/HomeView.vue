<template>
  <div class="home">
    <FilterNav @filterBy="current = $event" :current="current" />

    <div v-if="projects.length">
      <div v-for="project in handleFilterProjects" :key="project.id">
        <ProjectItem 
          :project="project" 
          @delete="handleDelete" 
          @complete="handleComplete" 
        />
      </div>
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav.vue'
import ProjectItem from '../components/ProjectItem.vue'

export default {
  name: 'HomeView',
  components: { ProjectItem, FilterNav },
  data() {
    return {
      projects: [],
      url: 'http://localhost:3000/projects',
      current: 'all'
    }
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter(p => p.id !== id)
    },
    handleComplete(id) {
      const toggledProject = this.projects.find(p => p.id === id)
      toggledProject.complete = !toggledProject.complete
    }
  },
  computed: {
    handleFilterProjects() {
      if(this.current === 'completed') return this.projects.filter(p => p.complete)
      if(this.current === 'undone') return this.projects.filter(p => !p.complete)

      return this.projects
    }
  },
  mounted() {
    fetch(this.url)
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err))
  }
}
</script>