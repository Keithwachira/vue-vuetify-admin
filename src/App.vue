<template>
  <v-app>
    <v-navigation-drawer
      persistent
      :mini-variant="miniVariant"
      :clipped="clipped"
      v-model="drawer"
      enable-resize-watcher
      fixed
      app
    >

      <v-list>
        <v-list-group
          v-for="item in items"
          v-model="item.active"
          :key="item.title"
          :prepend-icon="item.action"
          no-action v-if="item.items"
        >
          <v-list-tile slot="activator">
            <v-list-tile-content>
              <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>

          <v-list-tile
            v-for="subItem in item.items"
            :to="subItem.to"
            :key="subItem.title"
            @click="" v-if="item.items"
          >
            <v-list-tile-content>
              <v-list-tile-title>{{ subItem.title }}</v-list-tile-title>
            </v-list-tile-content>

            <v-list-tile-action>
              <v-icon>{{ subItem.action }}</v-icon>
            </v-list-tile-action>
          </v-list-tile>
        </v-list-group>


        <v-divider
          v-else-if="item.divider"
          :key="index"
        ></v-divider>


        <v-subheader
          v-else-if="item.header"
          :key="item.header"
        >
          {{ item.header }}
        </v-subheader>





        <v-list-tile
          router

          :key="item.title"
          :to="item.to"


          exact v-else
        >
          <v-list-tile-action>
            <v-icon>{{ item.action }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>


            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>


        </v-list-tile>


      </v-list>


    </v-navigation-drawer>
    <v-toolbar
      app
      color="primary"
      dark
      :clipped-left="clipped"
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer">

      </v-toolbar-side-icon>
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'">

        </v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>web</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>remove</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title">

      </v-toolbar-title>
      <v-spacer>

      </v-spacer>

    </v-toolbar>
    <v-content>
      <router-view/>
    </v-content>

    <v-footer :fixed="fixed" app>
      <span>&copy; 2018 </span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        clipped: true,
        drawer: true,
        fixed: false,


        items: [
          {
            action: 'dashboard',
            title: 'DashBoard',
            to: '/'

          },


          {
            action: 'trending_up',
            title: 'Charts',
            to: '/'

          },




          {header: 'Ui Elements'},

          {divider: true},


          {
            action: 'dashboard',
            title: 'Data Tables',
            to: '/tables'

          },

          {
            action: 'dashboard',
            title: 'Editor',
            to: '/editor'

          },




          {
            action: 'note',
            title: 'Pages',

            items: [
              {title: 'Login', to: '/admin/users/allusers'},
              {title: 'Sign Up', to: '/admin/users/allusers'},
              {title: '404', to: '/admin/users/allusers'},
              {title: '403', to: '/admin/users/blocked'},
              {title: '500', to: '/admin/users/blocked'},

            ]
          },



        ],


        miniVariant: false,
        right: true,
        rightDrawer: false,
        title: 'Vue Admin DashBoard'
      }
    },
    name: 'App'
  }
</script>
