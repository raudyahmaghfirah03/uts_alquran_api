<script>
export default {
  name: "FooterItem",
};
</script>

<template>
  <footer class="text-white p-1">
    <div class="d-flex justify-content-around">
      <p>2022 © Raudyah Maghfirah</p>
    </div>
  </footer>
</template>

<style scoped>
footer {
  font-family: Joyce;
  background-color: #90c6ba;
  position: fixed;
  bottom: 0;
  width: 100%;
  animation: hue-rotate 2s linear infinite alternate;
}
@keyframes hue-rotate {
  to {
    filter: hue-rotate(90deg);
  }
}
</style>