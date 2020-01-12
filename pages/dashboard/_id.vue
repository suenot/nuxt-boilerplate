<template>
  <div class="">
  <client-only>
  <v-btn @click="addWidget()">+</v-btn>
    <grid-layout :layout.sync="layout" :col-num="grid_settings.col_num" :row-height="grid_settings.row_height"
      :is-draggable="grid_settings.is_draggable" :is-resizable="grid_settings.is_resizable" :is-mirrored="false"
      :vertical-compact="grid_settings.vertical_compact" :margin="grid_settings.margin" :use-css-transforms="true"
    >
      <grid-item v-for="widget in layout" :x="widget.x" :y="widget.y" :w="widget.w" :h="widget.h" :i="widget.i" :key="widget.i"
        :class="`widget ${widget.fullscreen ? 'fullscreen' : ''}`">
        <v-card class="mx-auto widget" outlined>
          <v-card-actions v-if="!grid_settings.header_hidden">
            <v-btn text>{{widget.component}}</v-btn>
            <v-spacer></v-spacer>
            <!-- <v-btn icon><v-icon>mdi-timer-10</v-icon></v-btn> -->
            <!-- <v-btn icon><v-icon>mdi-magnify</v-icon></v-btn> -->
            <v-menu v-model="widget.dropdown"
              :disabled="disabled"
              :absolute="absolute"
              :open-on-hover="openOnHover"
              :close-on-click="closeOnClick"
              :close-on-content-click="closeOnContentClick"
              :offset-x="offsetX"
              :offset-y="offsetY"
            >
              <template v-slot:activator="{ on }">
                <v-btn icon v-on="on">
                  <v-icon>mdi-dots-vertical</v-icon>
                </v-btn>
              </template>
              <v-list>
                <v-list-item :key="`action-fullscreen-${widget.i}`"  @click="widget.fullscreen = true" v-if="!widget.fullscreen">
                  <v-list-item-icon class="mr-3">
                    <v-icon>mdi-fullscreen</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <span>Fullscreen</span>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item :key="`action-fullscreen-exit-${widget.i}`"  @click="widget.fullscreen = false" v-else>
                  <v-list-item-icon class="mr-3">
                    <v-icon>mdi-fullscreen-exit</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <span>Exit fullscreen</span>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item :key="`action-settings-${widget.i}`" @click="1+1">
                  <v-list-item-icon class="mr-3">
                    <v-icon>mdi-settings</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <span>Settings</span>
                  </v-list-item-content>
                </v-list-item>
                <v-list-item :key="`action-delete-${widget.i}`"  @click="removeWidget(widget.i)">
                  <v-list-item-icon class="mr-3">
                    <v-icon class="red--text">mdi-delete</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content>
                    <span class="red--text">Remove</span>
                  </v-list-item-content>
                </v-list-item>
              </v-list>
            </v-menu>
          </v-card-actions>
          <div class="widget-body">
            <!-- <component :is="widget.component" :key="widget.i"></component> -->
            sdfsdfs sdfsdf sdfsdf
          </div>
        </v-card>
      </grid-item>
    </grid-layout>
  </client-only>
  </div>
</template>

<script>
// import VueGridLayout from 'vue-grid-layout'
// import FreelanceList from '@/components/FreelanceList.vue'
// import ProjectsList from '@/components/ProjectsList.vue'
// import StackedBars from '@/components/StackedBars.vue'
// import Bars from '@/components/Bars.vue'
// import Funnel from '@/components/Funnel.vue'
import uuidv1 from 'uuid/v1'
import _ from 'lodash'

var testLayout = [
  // {"x":0,"y":0,"w":12,"h":10,"i":"0", "component": "Bars", "dropdown": false, "fullscreen": false},
  // // {"x":2,"y":0,"w":12,"h":10,"i":"1", "component": "FreelanceList", "dropdown": false, "fullscreen": false},
  // {"x":4,"y":0,"w":12,"h":10,"i":"2", "component": "ProjectsList", "dropdown": false, "fullscreen": false},
  // {"x":8,"y":0,"w":12,"h":10,"i":"4", "component": "Funnel", "dropdown": false, "fullscreen": false},
]
export default {
  name: 'Grid',
  components: {
    // GridLayout: VueGridLayout.GridLayout,
    // GridItem: VueGridLayout.GridItem,
    // FreelanceList,
    // ProjectsList,
    // StackedBars,
    // Bars,
    // Funnel
  },
  data: () => ({
    fullscreen: false,
    layout: testLayout,
    grid_settings: {
      col_num: 12,
      row_height: 30,
      is_draggable: true,
      is_resizable: true,
      vertical_compact: true,
      margin: [20, 20],
      header_hidden: false,
      namespace: 'some'
    },
    // drop options
    disabled: false,
    absolute: false,
    openOnHover: false,
    closeOnClick: true,
    closeOnContentClick: true,
    offsetX: false,
    offsetY: true,
    //drop options end
  }),
  storage: {
    keys: ['layout', 'grid_settings'],
    namespace: 'grid'
  },
  mounted() {
    // console.log(this.$route.fullPath)
  },
  methods: {
    // resizedEvent: () => {
    //   window.dispatchEvent(new Event('resize'))
    // },
    removeWidget(widgetId) {
      console.log(widgetId)
      this.layout = _.filter(this.layout, function(widget) {
        return widget.i !== widgetId
      })
    },
    addWidget() {
      this.layout.push({"x":2,"y":0,"w":12,"h":10,"i":uuidv1(), "component": "FreelanceList", "dropdown": false, "fullscreen": false})
    }
  }
};
</script>

<style lang="sass">
.vue-grid-layout
  width: 100%
  margin: 0px 10px 0px 0px
  min-width: 100%
  margin-bottom: 40px
.widget
  width: 100%
  height: 100%
  max-width: 100%
  max-height: 100%
  display: flex
  flex-direction: column
  overflow-x: hidden
  overflow-y: auto
  .widget-body
    flex: 1 1 auto
    overflow-y: auto
    overflow-x: hidden
    position: relative
  &.fullscreen
    position: fixed !important
    z-index: 10000
    width: 100% !important
    height: 100% !important
    top: 0
    left: 0
    transform: translate3d(0px, 0px, 0px) !important
.vue-resizable-handle
  height: 42px !important
  width: 42px !important
</style>
