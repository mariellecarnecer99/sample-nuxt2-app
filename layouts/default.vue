<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer
        expand-on-hover
        rail
      >
        <v-list>
          <v-list-item
            prepend-avatar="https://randomuser.me/api/portraits/women/85.jpg"
            title="Sandra Adams"
            subtitle="sandradams@gmail.com"
          >
            <template v-slot:append>
              <v-btn
                variant="text"
                icon="mdi-logout"
                @click="logoutUser()"
              ></v-btn>
            </template>
          </v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item to="/" prepend-icon="mdi-home" title="Home" value="home"></v-list-item>
          <v-list-item to="/shared" prepend-icon="mdi-account-multiple" title="Shared with me" value="shared"></v-list-item>
          <v-list-item to="/starred" prepend-icon="mdi-star" title="Starred" value="starred"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-main>
          <slot />
      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
export default {
    data() {
        return {
            // userEmail: localStorage.getItem('userEmail')
        }
    },
    methods: {
        logoutUser() {
            const router = useRouter();
            router.push({path: "/login"});
            localStorage.removeItem('userEmail');
        }
    }
}
</script>