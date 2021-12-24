<template lang="pug">
v-app
  v-navigation-drawer(v-model="drawer" temporary app)
    v-list-item
      v-list-item-content
        v-list-item-title(class="text-h6") Application
        v-list-item-subtitle subtext
  v-app-bar(elevation="4" app)
    v-app-bar-nav-icon(@click.stop="drawer = !drawer")
  v-main
    Map
  v-footer(app)
</template>

<script>
import Map from './components/Map.vue'

export default {
  name: 'App',
  components: {
    Map
  },
  data: () => ({
    drawer: false,
  })
}
</script>
