<template>
  <v-card class="window-modal">
      <v-toolbar
              flat
              dark
      >
      </v-toolbar>
      <div class="container">
          <div class="table">
              <draggable class="list-group" :list="list1" group="people" @change="log">
                  <div
                          class="list-group-item"
                          v-for="(element) in list1"
                          :key="element.name"
                  >
                   <UserCard :name="element.name" :photo="element.photo" />
                  </div>
                  <div
                          slot="header"
                          class="btn-group list-group-item"
                          role="group"
                          aria-label="Basic example"
                  >
                      <v-btn
                              x-large
                              color="success"
                              dark
                              @click="logIn"
                      >
                          Авторизация <v-icon class="btn-icon">mdi-vk</v-icon>
                      </v-btn>
                  </div>
              </draggable>
          </div>
          <v-divider
                  v-if="!this.list1.length"
                  vertical
          ></v-divider>
          <div class="table">
              <draggable class="list-group" :list="list2" group="people" @change="log">
                  <div
                          class="list-group-item"
                          v-for="(element) in list2"
                          :key="element.name"
                  >
                      <UserCard :name="element.name" :photo="element.photo" />
                  </div>
                  <div
                          slot="header"
                          class="btn-group list-group-item"
                          role="group"
                          aria-label="Basic example"
                  >
                      <v-btn
                              x-large
                              color="success"
                              dark
                              @click="showFriends"
                      >
                          Сохранить <v-icon class="btn-icon">mdi-check mark</v-icon>
                      </v-btn>
                  </div>
              </draggable>
          </div>
      </div>
  </v-card>
</template>
<script>
  /* global VK */
  import draggable from 'vuedraggable';
  import UserCard from "./UserCard";
  export default {
    name: "two-lists",
    order: 1,
    components: {
      UserCard,
      draggable
    },
    data: () => ({
        list1: [],
        list2: [],
        userId: null,
        friends: null,
    }),
    methods: {
      add: function() {
        this.list.push({ name: "Juan" });
      },
      replace: function() {
        this.list = [{ name: "Edgard" }];
      },
      clone: function(el) {
        return {
          name: el.name + " cloned"
        };
      },
      log: function(evt) {
        window.console.log(evt);
      },
      logIn() {
          VK.Auth.login((data) => {
              VK.Api.call('friends.get', { user_id: data.session.user.id, fields: 'photo', v:"5.21" }, (r) => {
                  if(r.response) {
                      this.list1 = [];
                      r.response.items.forEach((item) => {
                          this.list1.push({ 'name': `${item.first_name} ${item.last_name}`, 'photo': `${item.photo}` });
                      });
                  }
              });
          });
      },
      showFriends() {
        console.log(this.list2);
      },
    },
  };
</script>

<style scoped>
  .window-modal {
    margin: 50px 150px 0 150px;
    background: url("https://cdn.vuetifyjs.com/images/parallax/material.jpg");
  }
  .container {
      display: flex;
      height: 750px;
      overflow: auto;
  }
  .table {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex-grow: 1;
    overflow: auto;
  }
  .list-group-item {
    margin: 15px 0 15px 0;
    cursor: move;
  }
  .btn-icon {
      left: 10px;
  }
</style>
