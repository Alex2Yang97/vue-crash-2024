<script>
export default {
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      tasks: ['task 1', 'task 2', 'task 3'],
      link: 'https://www.google.com'
    }
  },
  methods: {
    toggleStatus() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'inactive'
      } else {
        this.status = 'active'
      }
    },
  },
}
</script>


<template>
  <h1> {{ name }} </h1>
  <p v-if="status === 'active'">Status: Active</p>
  <p v-else-if="status === 'inactive'">Status: Inactive</p>
  <p v-else>Status: Unknown</p>

  <h3>Tasks</h3>
  <ul>
    <li v-for="task in tasks" :key="task"> {{ task }} </li>
  </ul>

  <!-- <a v-bind:href="link">Google</a> -->
  <a :href="link">Google</a>
  <br />
  <button @click="toggleStatus">Change Status</button>

</template>



