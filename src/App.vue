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


      <v-spacer></v-spacer>


      <v-menu offset-y origin="center center" class="elelvation-1" :nudge-bottom="14" transition="scale-transition">
        <v-btn icon flat slot="activator">
          <v-badge color="red" overlap>
            <span slot="badge">3</span>
            <v-icon medium>notifications</v-icon>
          </v-badge>
        </v-btn>
        <notification-list>

        </notification-list>

      </v-menu>




      <v-menu offset-y origin="center center" :nudge-bottom="10" transition="scale-transition">
        <v-btn icon large flat slot="activator">
          <v-avatar size="30px">
            <img src="https://avatars2.githubusercontent.com/u/8012032?s=460&v=4" alt="Michael Wang"/>
          </v-avatar>
        </v-btn>
        <v-list class="pa-0">
          <v-list-tile v-for="(item,index) in item" :to="!item.href ? { name: item.name } : null" :href="item.href" @click="item.click" ripple="ripple" :disabled="item.disabled" :target="item.target" rel="noopener" :key="index">
            <v-list-tile-action v-if="item.icon">
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-menu>


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

  import NotificationList from "../src/components/notifications/NotificationList";
  export default {
    components:{

      NotificationList
    },
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
            title: 'Components',

            items: [
              {title: 'Cards', to: '/admin/users/allusers'},
              {title: 'Sign Up', to: '/admin/users/allusers'},
              {title: '404', to: '/admin/users/allusers'},
              {title: '403', to: '/admin/users/blocked'},
              {title: '500', to: '/admin/users/blocked'},

            ]
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
