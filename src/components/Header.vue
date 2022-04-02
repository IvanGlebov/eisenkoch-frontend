<template>
  <div class="header">
    <div class="tokens-wrapper">
      <div class="tokens-earned-header">Заработал токенов:</div>
      <div class="tokens-earned-content">10,05</div>
    </div>
    <div class="header-title">
      робот, который печёт вафли
    </div>
    <div class="waffles-wrapper">
      <div class="waffles-baked-header">всего испёк вафель</div>
      <div class="waffles-baked-content">600</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "InfoHeader"
}
</script>

<style scoped>
.header {
  height: 170px;
  background-color: var(--color-dark-gray);
  display: flex;
  justify-content: center;
}
.header-title {
  background-image: url('../assets/header_back.svg');
  background-position: center;
  background-repeat: no-repeat;
  min-height: 100px;
  font-size: 3rem;
  padding: 20px 120px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
}

.tokens-wrapper, .waffles-wrapper {
  display: flex;
  flex-direction:column;
  justify-content: center;
  align-items: flex-end;
  margin-right: 20px;

  font-family: 'Roboto Mono', monospace;
  text-transform: uppercase;
  font-size: 1.7rem;
}
.waffles-wrapper {
  align-items: flex-start;
  margin-right: 0;
  margin-left: 20px;
}

.tokens-earned-header,
.tokens-earned-content,
.waffles-baked-header,
.waffles-baked-content {
  padding: 10px;
  background-color: var(--color-white);
}
.tokens-earned-header {
  transform: rotate(4deg) translatey(-2px);
}
.tokens-earned-content {
  transform: translatey(6px) translatex(-31px);
}
.waffles-baked-header {
  transform: rotate(-4deg) translatey(-2px);
}
.waffles-baked-content {
  transform: translateY(6px) translateX(31px);
}

</style>