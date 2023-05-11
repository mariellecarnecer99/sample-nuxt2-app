<template>
  <v-app dark>
    <v-navigation-drawer
      expand-on-hover
      rail
      app
    >
      <v-list>
        <v-list-item two-line>
          <v-list-item-action>
            <v-icon>mdi-account-circle</v-icon>
          </v-list-item-action>

          <v-list-item-content>
            <v-list-item-title>Sandra Adams</v-list-item-title>
            <v-list-item-subtitle>sandradams@gmail.com</v-list-item-subtitle>
          </v-list-item-content>
          
          <v-icon @click="logoutUser()">mdi-logout</v-icon>
        </v-list-item>
      </v-list>

      <v-divider></v-divider>

      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>{{item.title}}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      items: [
        {
          icon: 'mdi-home',
          title: 'Home',
          to: '/'
        },
        {
          icon: 'mdi-account-multiple',
          title: 'Shared with me',
          to: '/shared'
        },
        {
          icon: 'mdi-star',
          title: 'Starred',
          to: '/starred'
        }
      ]
    }
  },
  methods: {
    logoutUser() {
      this.$router.push({path: "/login"});
    }
  }
}
</script>
