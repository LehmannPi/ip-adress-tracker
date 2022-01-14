<template>
  <div class="info">
    <p class="info__title">IP Address Tracker</p>
    <input type="text" class="info__inp" />
		<div class="info__tracker">
			<div class="info__ip"></div>
			<div class="info__location"></div>
			<div class="info__timezone"></div>
			<div class="info__isp"></div>
		</div>
  </div>
</template>

<script>
export default {
  name: "InfoCard",
};
</script>

<style>
</style>