<template>
  <v-app dark>
    <v-navigation-drawer v-model="drawer" :clipped="clipped" fixed app>
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
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <v-toolbar-title>Brain-Food</v-toolbar-title>
      <v-spacer />
      <!-- logout button  -->
      <v-btn icon @click="logout">
        <v-icon>mdi-logout</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer v-model="rightDrawer" :right="right" temporary fixed>
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light> mdi-repeat </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: "mdi-chart-bubble",
          title: "Startseite",
          to: "/startseite",
        },
        {
          icon: "mdi-brain",
          title: "Ernährungsempfehlungen",
          to: "/ernährungsempfehlungen",
        },
        {
          icon: "mdi-noodles",
          title: "Rezepte",
          to: "/rezepte",
        },
        {
          icon: "mdi-pill-multiple",
          title: "Nahrungsergänzung",
          to: "/nahrungsergänzung",
        },
      ],
      get isLoggedIn() {
        return localStorage.getItem("isloggedin") == "true";
      },
      right: true,
      rightDrawer: false,
      title: "Vuetify.js",
    };
  },
  methods: {
    logout() {
      localStorage.removeItem("isloggedIn");
      this.$router.push("/");
    },
  },
};
</script>
