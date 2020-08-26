<template>
  <div class="container">
    <div class="row">
      <div class="col-5">
        <AddUser 
          @add-user="addUser"
          v-bind:users="users"
        />
      </div>
      <div class="col-12">
        <Table 
          v-bind:users="users"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AddUser from '@/components/AddUser.vue'
import Table from '@/components/Table.vue'

export default {
  data() {
    return {
      users: []
    }
  },
  methods: {
    addUser(user) {
      this.users.push(user)
    }
  },
  mounted() {
    fetch('./users.json')
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        for(let user of data.users) {
          this.users.push(user)
        }
      })
  },
  components: {
    AddUser, Table
  }
}
</script>

<style scope>
  .title {
    margin: 30px 0;
  }
</style>
