<template>
  <div id="app">
    <SearchBox @inputChange="fetchSearchedUser"></SearchBox>
    <UserList :users="usersList"></UserList>

    <div class="pagination-container">
      <a href="#" @click="changePage(1)">1</a>
      <a href="#" @click="changePage(2)">2</a>
      <a href="#" @click="changePage(3)">3</a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBox from "./components/SearchBox";
import UserList from "./components/UserList";
export default {
  data() {
    return {
      usersList: [],
      page: 1,
      per_page: 4
    };
  },
  name: "App",
  components: { UserList, SearchBox },
  methods: {
    fetchUsers() {
      axios
        .get(
          `https://reqres.in/api/users?page=${this.page}&per_page=${this.per_page}`
        )
        .then(response => {
          console.log(response);
          this.usersList = response.data.data;
        });
    },

    changePage(pageNumber) {
      this.page = pageNumber;
      console.log(this.page);
      this.fetchUsers();
    },

    fetchSearchedUser(name) {
      if (name.length > 3) {
        for (let i = 0; i < this.usersList.length; i++) {
          const element = this.usersList[i];
          if (
            (
              element.first_name.toLowerCase() +
              " " +
              element.last_name.toLowerCase()
            ).includes(name.toLowerCase())
          ) {
            this.usersList = [];
            this.usersList.push(element);
          }
        }
      }
      if (name == "") {
        this.fetchUsers();
      }
    }
  },

  created() {
    this.fetchUsers();
  }
};
</script>
  
<style>
.pagination-container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.pagination-container a {
  color: black;
  padding: 8px 16px;
  text-decoration: none;
  font-size: 18px;
}

.pagination-container a:hover {
  border-bottom: 1px solid red;
}
</style>
