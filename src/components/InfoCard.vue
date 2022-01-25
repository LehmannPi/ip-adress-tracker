<template>
  <c-box d="flex" flex-dir="column" align-items="center">
    <p class="info__title">IP Address Tracker</p>
    <!-- <c-input type="text" class="info__inp" /> -->
    <c-box
      d="flex"
      :width="[
        '88%', // base
        '555px',
      ]"
      pos="relative"
    >
      <c-input
        placeholder="Search for any IP address or domain"
        h="58px"
        rounded="12px"
      />
      <c-button
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
      >
        <c-icon fontSize="26px" name="chevron-right" />
      </c-button>
    </c-box>
    <!-- <c-box class="info__tracker"> -->
    <c-box
      d="flex"
      bg="white"
      rounded="12px"
      :mt="['23px', '48px']"
      :w="['87%', '78%']"
      zIndex="3"
      class="info-blocks-wrapper"
    >
      <!-- {{ info }}
      <p>{{ response }}</p> -->

      <div class="info__block">
        <p class="block__title">ip adress</p>
        <p class="block__value">b</p>
      </div>
			<div class="breakers"></div>
      <div class="info__block">
        <p class="block__title">location</p>
        <p class="block__value">b</p>
      </div>
			<div class="breakers"></div>
      <div class="info__block">
        <p class="block__title">timezone</p>
        <p class="block__value">b</p>
      </div>
			<div class="breakers"></div>
      <div class="info__block">
        <p class="block__title">isp</p>
        <p class="block__value">b</p>
      </div>
      <!-- <div class="info__ip"></div>
      <div class="info__location"></div>
      <div class="info__timezone"></div>
      <div class="info__isp"></div> -->
    </c-box>
  </c-box>
</template>

<script>
import { CInput, CBox, CButton, CIcon } from "@chakra-ui/vue";
import axios from "axios";

export default {
  name: "InfoCard",
  components: {
    CInput,
    CBox,
    CButton,
    CIcon,
  },
  data: () => ({
    // response: null,
    info: {},
    response: {},
  }),
  async mounted() {
    await axios
      .get("https://api.coindesk.com/v1/bpi/currentprice.json")
      .then((response) => (this.info = response.data))
      .catch((error) => console.log(error));

    this.response = this.info.time;
  },
};
</script>

<style>
</style>