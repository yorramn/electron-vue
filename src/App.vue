<template>
  <v-app style="-webkit-app-region: drag">
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant.sync="mini"
      permanent=""
      color="#2C3A47"
      dark
      app
    >
    <v-list-item class="px-2 pt-1">
      <v-list-item-avatar>
        <v-img src="./assets/logo.png" alt="admin" class="mx-auto"></v-img>
      </v-list-item-avatar>
      <v-list-item-title class="ml-4 text-capitalize">Yorramn</v-list-item-title>
    </v-list-item>
    <v-list shaped class="clickable">
      <template v-for="item in items">
        <v-list-group
          v-if="item.children"
          :key="item.text"
          v-model="item.model"
          :prepend-icon="item['icon-ctr']"
          :append-icon="item.model ? item.icon : item['icon-alt']"
          active-class="green--text"
        >
        <template v-slot:activator>
          <v-list-item-content>
            <v-list-item-title>{{item.text}}</v-list-item-title>
          </v-list-item-content>
        </template>
          <v-list-item
              v-for="(child, i) in item.children"
              :key="i"
              route :to="child.route"
              active-class="green--text"
              class="ml-4"
          >
            <v-list-item-action v-if="child.icon">
              <v-icon>{{child.icon}}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title>{{child.text}}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-group>
        <v-list-item
            v-else
            :key="item.text"
            active-class="green--text"
            route
            :to="item.route"
        >
          <v-list-item-icon>
            <v-icon>{{item.icon}}</v-icon>
          </v-list-item-icon>
          <v-list-item-title>{{item.text}}</v-list-item-title>
        </v-list-item>
      </template>
    </v-list>
    </v-navigation-drawer>
    <v-app-bar
      app
      color="#2C3A47"
      dark
    >
      <v-app-bar-nav-icon @click.stop="mini = !mini" class="clickable"></v-app-bar-nav-icon>
      <v-toolbar-title style="width: 300px" class="ml-0 pl-4">
        <span class="hidden-sm-and-down">App</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon v-on:click="logout"><v-icon>mdi-logout</v-icon></v-btn>
    </v-app-bar>
    <v-content>
      <v-container class="scroll-y" fluid>
        <v-row align="center" justify="center">
          <router-view></router-view>
        </v-row>
      </v-container>
    </v-content>
    <v-btn
           bottom
           color="pink"
           dark
           fab
           fixed
           right
           @click="toTop()"
           class="clickable"
    >
      <v-icon>mdi-chevron-up</v-icon>
    </v-btn>
  </v-app>
</template>

<script>

export default {
  name: 'App',
  props: {
    source: String
  },
  components: {

  },
  data: () => ({
    drawer: null,
    mini: false,
    fab: false,
    items: [
      {icon : 'mdi-home', text : 'Dashboard', route: '/'},
      {
        icon : 'mdi-chevron-up',
        'icon-alt': 'mdi-chevron-down',
        'icon-ctr' : 'mdi-cart-arrow-right',
        text : 'Orders',
        model: false,
        children: [
          {icon : 'style', text : 'Type', route: '/type'},
          {icon : 'atm', text : 'Mark', route: '/mark'},
        ]
      },
      {
        icon : 'mdi-chevron-up',
        'icon-alt': 'mdi-chevron-down',
        'icon-ctr' : 'mdi-cart-arrow-right',
        text : 'Trackin',
        model: false,
        children: [
          {icon : 'mdi-tooltip-account', text : 'Locate', route: '/locate'},
          {icon : 'mdi-printer', text : 'Print', route: '/print'}
        ],
      },
      {icon : 'mdi-finance', text : 'Revenue', route: '/revenue'},
      {icon : 'mdi-chart-pie', text : 'Analytics', route: '/chart'},
      {icon : 'mdi-magnify', text : 'Search', route: '/recherche'},

    ]
  }),
  methods: {
    toTop(){
      this.$vuetify.goTo(0)
    }
  }
};
</script>
<style>
.clickable{
  -webkit-app-region: no-drag
}
</style>