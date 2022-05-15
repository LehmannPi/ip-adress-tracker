<template>
  <CBox d="flex" flex-dir="column" align-items="center">
    <CText class="info__title">IP Address Tracker</CText>
    <CBox
      d="flex"
      :width="[
        '88%', // base
        '555px',
      ]"
      pos="relative"
    >
      <CInput
        placeholder="Search for any IP address or domain"
        h="58px"
        p="24px"
        rounded="12px"
        fontSize="18px"
        style="z-index: 3"
        v-model="ipInput"
      />
      <CButton
        icon="chevron-right"
        class="btn_go"
        rounded="12px"
        roundedLeft="0"
        h="58px"
        w="58px"
        pos="absolute"
        right="0"
        bg="black"
        color="white"
        zIndex="10"
        @click="apiComm"
      >
        <c-icon fontSize="26px" name="chevron-right" />
      </CButton>
    </CBox>
    <CBox
      d="flex"
      bg="white"
      rounded="12px"
      :mt="['23px', '48px']"
      :w="['87%', '78%']"
      zIndex="3"
      class="info-blocks-wrapper"
    >
      <div class="info__block">
        <CText class="block__title">ip adress</CText>
        <CText class="block__value">{{ this.ipDisplay }}</CText>
      </div>
      <div class="breakers"></div>
      <div class="info__block">
        <CText class="block__title">location</CText>
        <CText class="block__value">{{ this.location }}</CText>
      </div>
      <div class="breakers"></div>
      <div class="info__block">
        <CText class="block__title">timezone</CText>
        <CText class="block__value">{{ this.timezone }}</CText>
      </div>
      <div class="breakers"></div>
      <div class="info__block">
        <CText class="block__title">isp</CText>
        <CText class="block__value">{{
          this.isp || "Could not determine"
        }}</CText>
      </div>
    </CBox>
  </CBox>
</template>

<script>
import { CInput, CBox, CButton, CIcon, CText } from "@chakra-ui/vue";

export default {
  name: "InfoCard",
  components: {
    CInput,
    CBox,
    CButton,
    CIcon,
    CText,
  },
  data: () => ({
    url: `https://ipgeolocation.abstractapi.com/v1/?api_key=${process.env.VUE_APP_ABSTRACT}`,
    ipInput: "",
    ipDisplay: "",
    location: "",
    timezone: "",
    isp: "",
    longitude: 0,
    latitude: 0,
  }),
  methods: {
    locationFormatter: (city, name, postal) => {
      return city + ", " + name + " " + postal;
    },
    regionFormatter: (time) => {
      if (time.toString().length < 3 && time < 0) {
        return "GMT -0" + time.toString().slice(1) + ":00";
      } else if (time.toString().length < 2 && time > 0) {
        return "GMT 0" + time.toString() + ":00";
      } else {
        return "GMT " + time.toString() + ":00";
      }
    },
    async apiComm() {
      var aux;
      var flag = false; // ativa para campo nulo
      const axios = require("axios").default;
      if (this.ipInput) {
        aux = this.url + "&ip_address=" + this.ipInput;
      }
      if (!this.ipInput) {
        aux = this.url;
        flag = true;
      }
      console.log(aux);
      await axios(aux)
        .then((response) => {
          console.log(response.data);
          this.ipDisplay = response.data.ip_address;
          this.location = response.data.city
            ? this.locationFormatter(
                response.data.city,
                response.data.region_iso_code,
                response.data.postal_code
              )
            : "Could not determine";
          this.timezone = response.data.timezone.gmt_offset
            ? this.regionFormatter(response.data.timezone.gmt_offset)
            : "Could not determine";
          this.isp = response.data.connection.autonomous_system_organization;
          this.latitude = response.data.latitude;
          this.longitude = response.data.longitude;
        })
        .catch((error) => {
          alert("Too many requests, wait a little bit before trying again.");
          console.log(error);
        });
      if (flag) this.ipInput = this.ipDisplay;
      this.$emit("renderMap", this.latitude, this.longitude, this.location);
    },
    async fullProcedure() {},
  },
  async mounted() {
    await this.apiComm();
  },
};
</script>

<style>
</style>