<template>
  <v-app id="sandbox" :dark="true">

    <!-- left drawer start -->
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="primaryDrawer.clipped"
      :floating="primaryDrawer.floating"
      :mini-variant="primaryDrawer.mini"
      app
      overflow
    >
      <v-list>
        <v-list-item-group>
          <draggable v-model="navigationLeftTop" group="navigation">
            <template v-for="item in navigationLeftTop">
              <router-link :to="item.link" :key="`navigationLeftTop-${item.link}`" tag="div">
                <v-list-item>
                  <v-tooltip right>
                    <template v-slot:activator="{ on }">
                      <v-list-item-content v-on="on" class="mx-auto">
                        <v-icon v-text="item.icon">mdi-heart</v-icon>
                      </v-list-item-content>
                    </template>
                    <span v-text="item.tooltip"></span>
                  </v-tooltip>
                </v-list-item>
                <v-divider></v-divider>
              </router-link>
            </template>
          </draggable>

          <v-spacer></v-spacer>
          <v-divider></v-divider>
          <draggable v-model="navigationLeftBottom" group="navigation">
            <template v-for="item in navigationLeftBottom">
              <router-link :to="item.link" :key="`navigationLeftBottom-${item.link}`" tag="div">
                <v-list-item>
                  <v-tooltip right>
                    <template v-slot:activator="{ on }">
                      <v-list-item-content v-on="on" class="mx-auto">
                        <v-icon v-text="item.icon">mdi-heart</v-icon>
                      </v-list-item-content>
                    </template>
                    <span v-text="item.tooltip"></span>
                  </v-tooltip>
                </v-list-item>
                <v-divider></v-divider>
              </router-link>
            </template>
          </draggable>
        </v-list-item-group>


      </v-list>
    </v-navigation-drawer>
    <!-- left drawer end -->

    <!-- right drawer start -->
    <v-divider></v-divider>
    <v-navigation-drawer
      v-model="primaryDrawer.model"
      :clipped="primaryDrawer.clipped"
      :floating="primaryDrawer.floating"
      :mini-variant="primaryDrawer.mini"
      app
      overflow
      right
    >
      <v-list>
        <v-list-item-group>
          <draggable v-model="navigationRightTop" group="navigation">
            <template v-for="item in navigationRightTop">
              <router-link :to="item.link" :key="`menu-${item.link}`" tag="div">
                <v-list-item>
                  <v-tooltip left>
                    <template v-slot:activator="{ on }">
                      <v-list-item-content v-on="on" class="mx-auto">
                        <v-icon v-text="item.icon">mdi-heart</v-icon>
                      </v-list-item-content>
                    </template>
                    <span v-text="item.tooltip"></span>
                  </v-tooltip>
                </v-list-item>
                <v-divider></v-divider>
              </router-link>
            </template>
          </draggable>
          <v-spacer></v-spacer>
          <v-divider></v-divider>
          <draggable v-model="navigationRightBottom" group="navigation">
            <template v-for="item in navigationRightBottom">
              <router-link :to="item.link" :key="`menu-${item.link}`" tag="div">
                <v-list-item>
                  <v-tooltip left>
                    <template v-slot:activator="{ on }">
                      <v-list-item-content v-on="on" class="mx-auto">
                        <v-icon v-text="item.icon">mdi-heart</v-icon>
                      </v-list-item-content>
                    </template>
                    <span v-text="item.tooltip"></span>
                  </v-tooltip>
                </v-list-item>
                <v-divider></v-divider>
              </router-link>
            </template>
          </draggable>
        </v-list-item-group>




      </v-list>
    </v-navigation-drawer>
    <!-- right drawer end -->
    <v-content>
      <nuxt />
    </v-content>

  </v-app>
</template>

<script>
import draggable from 'vuedraggable'

export default {
  // storage: {
  //   keys: ['navigationLeftTop', 'navigationLeftBottom', 'navigationRightTop', 'navigationRightBottom'],
  //   namespace: 'app'
  // },
  data: () => ({
    navigationLeftTop: [
      {
        link: '/crypto',
        tooltip: 'CryptoHome',
        icon: 'mdi-airplane',
      },
      {
        link: '/freelance',
        tooltip: 'FreelanceHome',
        icon: 'mdi-heart',
      },
      {
        link: '/freelance/project',
        tooltip: 'ProjectPage',
        icon: 'mdi-heart',
      },
    ],
    navigationLeftBottom: [
      {
        link: '/signals',
        tooltip: 'Signals',
        icon: 'mdi-chess-pawn',
      },
      {
        link: '/signal',
        tooltip: 'Signal',
        icon: 'mdi-chess-bishop',
      },
      {
        link: '/magnify',
        tooltip: 'Magnify',
        icon: 'mdi-magnify',
      },
    ],
    navigationRightTop: [
      {
        link: '/grid',
        tooltip: 'Grid',
        icon: 'mdi-chess-rook',
      }
    ],
    navigationRightBottom: [],
    primaryDrawer: {
      model: null,
      clipped: false,
      floating: false,
      mini: true,
    },
    footer: {
      inset: true,
    },
  }),
  mounted() {
    // this.$vuetify.theme.dark = true
    // console.log(this.$vuetify.theme.isDark)
  },
  components: {
    draggable,
  },
  methods: {}
}
</script>
<style lang="sass" scoped>
.v-list
  padding: 0
.v-item-group
  height: 100vh
  display: flex
  flex-direction: column
</style>

<style lang="sass">
// .v-data-table thead tr th
//   white-space: nowrap
</style>

<style lang="sass">
.v-input__append-inner
  .v-btn
    position: relative
    top: -5px
</style>
