<template>
  <div class="col-md-12">
    <div class="form-group">
      <input type="text" class="form-control" v-model="search" placeholder="Search by user name">
    </div>
    <div class="table-responsive">
      <table class="table table-striped table-bordered" style="width:100%">
          <thead width="400px">
              <tr>
                  <th scope="col">#</th>
                  <th scope="col" @click="sort('name')">Name <i class="fas fa-sort-alpha-down float-right"></i></th>
                  <th scope="col" @click="sort('email')">Email<i class="fas fa-sort-alpha-down float-right"></i></th>
                  <th scope="col">City</th>
                  <th scope="col">Phone </th>
              </tr>
          </thead>
          <tbody>
              <tr v-for="(user, index) in (sortedActivity, filteredList)" :key="index">
                <td>{{index + 1}}</td>
                <td>{{user.name}}</td>
                <td>{{user.email}}</td>
                <td>{{user.address.city}}</td>
                <td>{{user.phone}}</td>
              </tr>
          </tbody>
      </table>
    </div>
    <p><a href="" class="float-left"><i class="fas fa-arrow-left"></i> Previous</a> <a href="" class="float-right">Next <i class="fas fa-arrow-right"></i></a></p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data: () => ({
    users: [],
    currentSort:'name',
    currentSortDir:'asc',
    search: ''
  }),

  methods:{
    sort:function(s) {
      if(s === this.currentSort) {
        this.currentSortDir = this.currentSortDir==='asc'?'desc':'asc';
      }
      this.currentSort = s;
    },
  },

  computed: {
    sortedActivity:function() {
      return this.users.sort((a,b) => {
        let modifier = 1;
        if(this.currentSortDir === 'desc') modifier = -1;
        if(a[this.currentSort] < b[this.currentSort]) return -1 * modifier;
        if(a[this.currentSort] > b[this.currentSort]) return 1 * modifier;
        return 0;
      });
    },

    filteredList () {
      return this.users.filter((data) => {
          return data.name.toLowerCase().match(this.search.toLowerCase())
      });
    }
  },

  created () {
    axios.get('https://jsonplaceholder.typicode.com/users')
      .then(response => {
        this.users = response.data
      })
  },

}
</script>

<style>
.success {
  background-color: #04f90063;
}

.fail {
  background-color: #ff000063;
}

th {
  cursor:pointer;
  /* width: 500px !important; */
  white-space: nowrap;
}

tr {
  white-space: nowrap;
}

.first-col {
    position: absolute;
    width: 5em;
    margin-left: -5em;
}

</style>
