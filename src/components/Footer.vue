<template>
  <footer class="footer">
    <div class="footer-video-wrapper">
      <div class="qr-code-wrapper">
        <img :src="videoQr" alt="Video qr code">
      </div>
      <div class="footer-video-content">
      </div>
    </div>
    <div class="footer-links-wrapper">
      <div class="qr-code-wrapper">
        <img :src="coffeenomicaQr" alt="coffeenomica qr code">
        <div class="qr-footnote" id="coffeenomica">coffeenomica.ru</div>
      </div>
      <div class="qr-code-wrapper">
        <img :src="multiAgentQr" alt="multi-agent qr code">
        <div class="qr-footnote" id="multiAgent">multi-agent.ru</div>
      </div>
      <div class="qr-code-wrapper">
        <img :src="robonomicsNetworkQr" alt="robonomics network qr code">
        <div class="qr-footnote" id="robonomicsNetwork">robonomics.network</div>
      </div>
    </div>
    <div class="footer-logo-wrapper">
      <img :src="logoGear" alt="gear logotype part">
      <img :src="logoName" alt="name logotype part">
<!--      <img :src="logoSvg" alt="Coffeenomics logo">-->

    </div>
  </footer>
</template>

<script>
export default {
  name: "FooterLinks",
  data() {
    return {
      logoSvg: require('../assets/cofeenomics_logo.svg'),
      videoQr: require('../assets/videoQr.svg'),
      coffeenomicaQr: require('../assets/coffeenomicaRuQr.svg'),
      multiAgentQr: require('../assets/multiAgentQr.svg'),
      robonomicsNetworkQr: require('../assets/robonomicsNetworkQr.svg'),
      logoGear: require('../assets/logo_gear.svg'),
      logoName: require('../assets/logo_name.svg')
    }
  }
}
</script>

<style scoped>

.footer {
  height: 189px;
  background-color: var(--color-dark-gray);
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}

.footer-video-wrapper {
  display: flex;
  padding: 30px;
  height: 99px;
}
.footer-video-content {
  margin-left: 20px;
  width: 216px;
  background-color: var(--color-black);
  height: 129px;
}
.qr-code-wrapper {
  height: 69px;
  background-color: var(--color-black);
  padding: 30px;
  position: relative;
}
.qr-code-wrapper > img {
  height: 69px;
}

.footer-links-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
}

.qr-footnote {
  background-color: var(--color-blue-light);
  text-transform: uppercase;
  font-family: 'Roboto Mono', monospace;
  color: var(--color-white);
  position: absolute;
  padding: 5px;
}

.qr-footnote#coffeenomica{
  left: 35px;
  transform: rotate(-4deg);
  top: 109px;
}

.qr-footnote#multiAgent {
  width: 130px;
  left: 35px;
  transform: rotate(3deg);
  top: 109px;
}

.qr-footnote#robonomicsNetwork {
  top: 109px;
  left: 30px;
}

.footer-logo-wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 30px;
  position: relative;
}
.footer-logo-wrapper > img {
  position: absolute;
  height: 129px;
}

.footer-logo-wrapper > img:nth-child(1) {
  right: 95px;
  animation: 6s rotate linear infinite;
}

.footer-logo-wrapper > img:not(:nth-child(1)) {
  top: 50px;
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

</style>