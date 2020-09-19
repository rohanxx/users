<template>
  <div class="main">
    <ul>
      <li v-for="user in users" :key="user.id" class="align" @click="openModal(user)">
        <img :src="user.avatar" />
        <div>
          <h3>{{user.first_name}} {{ user.last_name }}</h3>
        </div>
      </li>
    </ul>

    <div class="user-modal" v-if="showModal">
      <img class="user-image" :src="modalData.avatar" />
      <div class="model-content">
        <span class="close" @click="showModal = !showModal">&#10006;</span>
        Name: {{ modalData.first_name }} {{ modalData.last_name }}
        <br />
        Email: {{ modalData.email }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showModal: false,
      modalData: []
    };
  },
  methods: {
    openModal(user) {
      this.showModal = true;
      this.modalData = user;
    }
  },
  name: "UserList",
  props: ["users"]
};
</script>

<style scoped>
.align {
  display: flex;
  align-items: center;
  width: 30%;
  margin: 25px auto;
}

.align:hover {
  background-color: #d6d6c2;
  cursor: pointer;
}

.align img {
  margin-right: 2rem;
  height: 100px;
  width: 100px;
  border-radius: 100px;
}
.main {
  position: relative;
}

.user-modal {
  background-color: aqua;
  height: 18rem;
  width: 45rem;
  display: flex;
  align-items: center;
  padding: 15px;
  justify-content: space-around;
  border-radius: 20px;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}

.close {
  cursor: pointer;
  position: absolute;
  top: 20px;
  right: 20px;
  font-size: 17px;
}

.user-image {
  border-radius: 100px;
}

.model-content {
  font-size: 18px;
  font-weight: 700;
}

.mr-3 {
  height: 100px;
}

@media (max-width: 800px) {
  .align {
    flex-direction: column;
  }
}

@media (max-width: 810px) {
  .user-modal {
    display: flex;
    flex-direction: column;
    width: 400px;
  }
}

@media (max-width: 450px) {
  .user-modal {
    width: 250px;
  }
}
</style>