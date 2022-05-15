<template>
  <div class="container">
    <div class="background">
      <img
        src="@/../images/pattern-bg.png"
        alt="Blue Background Image"
        class="background__image"
      />
    </div>
    <InfoCard @renderMap="setCoordinates" />
    <div class="map-container">
      <l-map id="map" :zoom="zoom" :center="center" :options="mapOptions">
        <l-tile-layer :url="url" />
        <l-marker :lat-lng="withPopup">
          <l-popup>{{ this.location }}</l-popup>
        </l-marker>
      </l-map>
    </div>
  </div>
</template>

<script>
import InfoCard from "../components/InfoCard.vue";
import { latLng } from "leaflet";

export default {
  components: { InfoCard },
  name: "Main",
  data() {
    return {
      zoom: 13,
      center: latLng(0, 0),
      withPopup: latLng(0, 0),
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      mapOptions: {
        zoomSnap: 0.5,
      },
      location: "",
    };
  },
  methods: {
    async setCoordinates(lat, lng, loc) {
      console.log("PASSED THROUGH: ", lat, lng, loc);
      this.center = latLng(lat, lng);
      this.withPopup = latLng(lat, lng);
      this.location = loc;
    },
  },
};
</script>

<style>
</style>