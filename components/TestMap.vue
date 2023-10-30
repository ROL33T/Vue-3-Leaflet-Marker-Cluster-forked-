<template>
  <l-map
    ref="map"
    :max-zoom="19"
    :zoom="zoom"
    :center="{ lat: 51.289404225298256, lng: 9.697202050919614 }"
    @ready="onLeafletReady"
  >
    <template v-if="leafletReady">
      <l-tile-layer :url="url" />
    </template>
  </l-map>
</template>
<script>
import "leaflet/dist/leaflet.css";

import { LMap, LMarker, LTileLayer } from "@vue-leaflet/vue-leaflet/src/lib";
import MarkerCluster from "./MarkerCluster.vue";

export default {
  components: {
    LMap,
    LTileLayer,
    LMarker,
    MarkerCluster,
  },

  data() {
    return {
      url: "https://{s}.tile.osm.org/{z}/{x}/{y}.png",
      zoom: 1,

      leafletReady: false,
      leafletObject: null,

      visible: false,
    };
  },

  methods: {
    async onLeafletReady() {
      await this.$nextTick();
      this.leafletObject = this.$refs.map.leafletObject;
      this.leafletReady = true;
    },
  },
};
</script>
