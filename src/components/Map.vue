<template lang="pug">
v-card(
  class="mx-auto"
  style="height: 100%; width: 80%;"
)
  v-row(no-gutters align="center" id="title-print")
    v-card-title Leaflet Map Practice
    v-btn(@click="print('map-print')" class="ml-5") Print Map
    v-btn(@click="print('title-print')" class="ml-5") Print Title
  LMap(
    id="map-print"
    style="height: 90%"
    :zoom="zoom"
    :center="center"
    @update:center="centerUpdate"
    @update:zoom="zoomUpdate"
    :options="{ attributionControl: false }"
  )
    LTileLayer(:url="url")
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer } from "vue2-leaflet";

export default {
  name: "Example",
  components: {
    LMap,
    LTileLayer,
  },
  data() {
    return {
      zoom: 10,
      center: latLng(34.543328, 135.2108),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      withPopup: latLng(47.41322, -1.219482),
      currentZoom: 11,
      currentCenter: latLng(47.41322, -1.219482),
    };
  },
  methods: {
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    print(elementId) {
      const prtHtml = document.getElementById(elementId).innerHTML

      let stylesHtml = ''
      for (const node of [...document.querySelectorAll('link[rel="stylesheet"], style')]) {
        stylesHtml += node.outerHTML
      }

      const WinPrint = window.open('', '', 'left=0,top=0,width=800,height=900,toolbar=0,scrollbars=0,status=0');

      WinPrint.document.write(`
        <!DOCTYPE html>
        <html>
          <head>
            ${stylesHtml}
          </head>
          <body>
            ${prtHtml}
          </body>
        </html>`
      );

      WinPrint.document.close();
      WinPrint.focus();
      WinPrint.print();
      // WinPrint.close();
    }
  }
};
</script>

<style>
.vue2leaflet-map {
  z-index: 1;
}
</style>
