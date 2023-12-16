<template>
  
    <transition-group tag="ul" name="user-list">
      <li v-for="user in users" :key="user" @click="removeUser(user)">
        {{ user }}
      </li>
    </transition-group>
  <div>
    <input type="text" ref="userNameInput" />
    <button @click="addUser">add user</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: ['Paweł', 'Grześ', 'Donald', 'Józef', 'Tomek'],
    };
  },
  methods: {
    addUser() {
      const enteredUserName = this.$refs.userNameInput.value;
      this.users.unshift(enteredUserName);
    },
    removeUser(user) {
      this.users = this.users.filter((usr) => usr !== user);
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
}
li {
  border: 1px solid red;
  text-align: center;
  padding: 1em;
}

.user-list-enter-from,.user-list-leave-to{
    overflow: 0;
    transform: translateX(-30px);
}
.user-list-enter-active{
    transition: all 1s ease-in;
}

.user-list-leave-active{
    transition: all 1s ease-out;
    position: absolute;
}
.user-list-enter-to, .user-list-leave-from{
    overflow: 1;
    transform: translateX(0);
}

.user-list-move{
    transition: transform .8s ease;
}
</style>
