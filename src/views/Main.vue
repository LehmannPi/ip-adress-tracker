<template>
  <div class="container">
    <div class="background">
			<img src="@/../images/pattern-bg.png" alt="Blue Background Image" class="background__image">
		</div>
		<InfoCard />
    <div class="map"></div>
  </div>
</template>

<script>
import InfoCard from '../components/InfoCard.vue';

export default {
  components: { InfoCard },
  name: "Main",
};
</script>

<style>
</style>