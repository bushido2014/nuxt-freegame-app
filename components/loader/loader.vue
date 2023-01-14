<template>
  <div class="loading">
    <span></span>
  </div>
</template>

<style scoped>
.loading {
  height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
@keyframes circle-loading {
  to {
    transform: rotateZ(360deg);
  }
}
.loading span {
  display: block;
  width: 90px;
  height: 90px;
  border-radius: 50%;
  border: 4px solid transparent;
  border-top-color: #fe4141;
  animation: circle-loading 1200ms ease infinite;
}
</style>
