<template>
  <footer class="footer">
    <div class="footer-video-wrapper">
      <div class="qr-code-wrapper">
        <img :src="videoQr" alt="Video qr code">
      </div>
      <div class="footer-video-content">
        <video width="170" height="85" autoplay muted loop>
          <source :src="video" type="video/mp4">
        </video>
        <!-- <iframe src="https://www.youtube.com/embed/UKAM6_tFuXk?version=3&playlist=UKAM6_tFuXk&loop=1&autoplay=1"
                title="Eisenkoch story"
                frameborder="0"
                allow="accelerometer; autoplay; loop; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                allowfullscreen>
        </iframe> -->
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
    </div>
  </footer>
</template>

<script>
import video from '../assets/video.mp4';

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
      logoName: require('../assets/logo_name.svg'),
      // videoLink: "https://www.youtube.com/watch?v=UKAM6_tFuXk",
      video,
    }
  },
  mounted() {
    console.log(this.$data.video);
  }
}
</script>

<style scoped>

.footer {
  /*height: 134px;*/
  min-height: 15vh;
  background-color: var(--color-dark-gray);
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  z-index: 1;
}

.footer-video-wrapper {
  display: flex;
  padding: 2vh;
  height: 11vh;
}

.footer-video-content {
  margin-left: 20px;
  width: 216px;
  /*background-color: var(--color-black);*/
  height: 11vh;
}

.footer-video-content > iframe {
  height: inherit;
  width: inherit;
}

.qr-code-wrapper {
  /*height: 61px;*/
  height: 7vh;
  background-color: var(--color-black);
  padding: 2vh;
  position: relative;
}

.qr-code-wrapper > img {
  /*height: 61px;*/
  height: 7vh;
}

.footer-links-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: row;
}

.footer-links-wrapper > .qr-code-wrapper {
  /*padding-bottom: 26px;*/
  padding-top: 1vh;
}

.footer-links-wrapper > .qr-code-wrapper > img {
  height: 7vh;
}

.qr-footnote {
  background-color: var(--color-blue-light);
  text-transform: uppercase;
  font-family: 'Roboto Mono', monospace;
  font-size: .6rem;
  color: var(--color-white);
  position: absolute;
  padding: 5px;
}

.qr-footnote#coffeenomica {
  left: 35px;
  transform: rotate(-4deg);
  top: 8.4vh;
}

.qr-footnote#multiAgent {
  width: 85px;
  left: 35px;
  transform: rotate(3deg);
  top: 8.4vh;
}

.qr-footnote#robonomicsNetwork {
  top: 8.4vh;
  left: 30px;
}

.footer-logo-wrapper {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  padding: 21px;
  position: relative;
}

.footer-logo-wrapper > img {
  position: absolute;
  height: 10vh;
  top: 2vh;
}

.footer-logo-wrapper > img:nth-child(1) {
  right: 7vh;
  animation: 6s rotate linear infinite;
}

.footer-logo-wrapper > img:not(:nth-child(1)) {
  right: 4.7vh;
  height: 7vh;
  top: 5vh;
}

@media screen and (min-height: 900px) {
  .qr-footnote {
    /*height: 50px;*/
    font-size: .8rem;
  }

  .qr-footnote#multiAgent {
    width: 110px;
  }
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