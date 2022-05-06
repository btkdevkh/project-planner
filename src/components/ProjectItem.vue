<template>
  <div class="project" :class="{ completed: project.complete }">
    <div class="actions">
      <h3 @click="showDetails = !showDetails">{{ project.title }}</h3>
      <div class="icons">
        <router-link :to="{ name: 'EditProjectView', params: { id: project.id } }">
          <span class="material-icons">edit</span>
        </router-link>
        <span class="material-icons" @click="deleteProject">delete</span>
        <span class="material-icons tick" @click="completeProject">done</span>
      </div>
    </div>
    <div v-if="showDetails" class="details">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['project'],
  data() {
    return {
      showDetails: false,
      url: 'http://localhost:3000/projects/' + this.project.id
    }
  },
  methods: {
    deleteProject() {
      fetch(this.url, {
        method: 'DELETE'
      })
      .then(() => this.$emit('delete', this.project.id))
      .catch(err => console.log(err))
    },
    
    completeProject() {
      fetch(this.url, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ complete: !this.project.complete })
      })
      .then(() => this.$emit('complete', this.project.id))
      .catch(err => console.log(err))
    }
  }
}
</script>

<style>
.project {
  padding: 10px 15px;
  margin-bottom: 10px;
  border-radius: 5px;
  background-color: #ddd;
  border-left: 5px solid crimson;
}

.project.completed {
  border-left: 5px solid green;
}

.project.completed .tick {
  color: green;
}

.actions{
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.actions h3 {
  cursor: pointer;
}

.icons span {
  cursor: pointer;
  margin-left: 10px;
  color: #908e8e;
}
</style>