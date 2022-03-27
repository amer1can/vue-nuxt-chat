<template>
  <div class="wrap flex flex-col">
    <div class="card">
      <div class="title">
        <h1>Login</h1>
      </div>
      <div class="text">
        <form ref="form">
          <input type="text" v-model="name">
          <input type="text" v-model="room">
          <button type="submit">Submit</button>
        </form>
      </div>
    </div>
  </div>
</template>

//https://stfalcon.com/ru/blog/post/chat-app-creation-vue.js-nuxt.js-node.js-socket.io-vue-socket.io-vuetify.js-technolog

<script>
import { mapMutations } from "vuex";
export default {
  name: 'IndexPage',
  data() {
    return {
      name: '',
      room: '',
      id: null
    }
  },
  mounted () {
    console.log('mounted')
  },
  methods: {
    ...mapMutations(["setUser"]),
    submit() {
      if (this.name.length > 0 && this.room.length > 0) {
        const user = {
          name: this.name,
          room: this.room,
          id: 0
        };
        this.$socket.emit("createUser", user, data => {
          user.id = data.id;
          this.setUser(user);
          this.$router.push("/chat");
        });
      }
    }
  }
}
</script>
