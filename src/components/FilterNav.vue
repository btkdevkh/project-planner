<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">All</button>
    <button @click="updateFilter('completed')" :class="{ active: current === 'completed' }">Completed</button>
    <button @click="updateFilter('undone')" :class="{ active: current === 'undone' }">Undone</button>
  </nav>
</template>

<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(by) {
      this.$emit('filterBy', by)
    }
  }
}
</script>

<style>
.filter-nav {
  text-align: left;
}

.filter-nav button {
  background: transparent;
  border: none;
  margin: 0 5px;
  text-transform: uppercase;
  font-weight: bold;
  color: #ddd;
  cursor: pointer;
}

.filter-nav button.active {
  color: green;
}
</style>