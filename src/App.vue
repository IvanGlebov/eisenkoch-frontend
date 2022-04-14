<template>
  <div class="app-wrapper">
    <info-header :base-url="baseUrl"/>
    <div class="main-content-wrapper">
      <oven-block :status="left_oven" variant="left" :time-left="left_oven_left"/>
      <div class="robo-arm-wrapper">
        <img :src="robo_arm" alt="robotic arm image">
        <!--        <img :src="robo_arm_top" alt="robotic arm image">-->
        <!--        <img :src="robo_arm_base" alt="robotic arm image">-->
      </div>
      <oven-block :status="right_oven" variant="right" :time-left="right_oven_left"/>
    </div>
    <footer-links/>
  </div>
</template>

<script>
import axios from 'axios'

import InfoHeader from './components/Header'
import FooterLinks from './components/Footer'
import OvenBlock from './components/Oven'


export default {
  name: 'App',
  components: {
    InfoHeader,
    FooterLinks,
    OvenBlock
  },
  data() {
    return {
      robo_arm: require('./assets/robo_arm.svg'),
      robo_arm_top: require('./assets/arm_top.svg'),
      robo_arm_base: require('./assets/arm_base.svg'),
      left_oven: 'available', //    4 states ->
      right_oven: 'available', // -> available, busy, cooking, finishing
      left_oven_baking_duration: 0,
      left_oven_left: 0,
      right_oven_baking_duration: 0,
      right_oven_left: 0,
      left_oven_status: false,
      right_oven_status: false,
      updateInterval: 1000,
      baseUrl: 'localhost:5000'
    }
  },
  methods: {
    getLeftOvenInfo() {
      axios.get(`http://${ this.$data.baseUrl }/status-left`)
          .then(res => {
            if (res.status !== 200)
              console.log('Error requesting oven info')
            else {
              this.$data.left_oven = res.data.status // Reading oven status
              this.$data.left_oven_left = res.data.baking_duration
              this.$data.left_oven_baking_duration = res.data.baking_duration // Reading baking duration
            }
          })
    },
    getRightOvenInfo() {
      axios.get(`http://${ this.$data.baseUrl }/status-right`)
          .then(res => {
            if (res.status !== 200)
              console.log('Error requesting oven info')
            else {
              this.$data.right_oven = res.data.status // Reading oven status
              this.$data.right_oven_left = res.data.baking_duration
              this.$data.right_oven_baking_duration = res.data.baking_duration // Reading baking duration
            }
          })
    },

    leftOvenWatcher() {
      switch (this.$data.left_oven) {
        case 'cooking':
          if (this.$data.left_oven_left <= 0) {
            this.$data.left_oven_left = 0
            this.$data.left_oven = 'busy'
          }
          this.$data.left_oven_left = this.$data.left_oven_left - this.$data.updateInterval / 1000
          break
        default:
          this.getLeftOvenInfo()
      }
    },
    rightOvenWatcher() {
      switch (this.$data.right_oven) {
        case 'cooking':
          if (this.$data.right_oven_left <= 0) {
            this.$data.right_oven_left = 0
            this.$data.right_oven = 'busy'
          }
          this.$data.right_oven_left = this.$data.right_oven_left - this.$data.updateInterval / 1000
          break
        default:
          this.getRightOvenInfo()
      }
    }
  },
  mounted() {
    setInterval(() => {
      this.leftOvenWatcher()
      this.rightOvenWatcher()

      // if(this.$data.left_oven === 'available') {
      //   this.$data.left_oven = 'busy'
      //   this.$data.right_oven = 'busy'
      // } else {
      //   this.$data.left_oven = 'available'
      //   this.$data.right_oven = 'available'
      // }
    }, 1000)

  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Yeseva+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@400;700&display=swap');

:root {
  --color-dark-gray: #181C20;
  --color-black: #000000;
  --color-yellow: #E2A307;
  --color-green: #598024;
  --color-white: #FFFFFF;
  --color-blue-light: #6E9BAA;
  --color-blue-verylight: #D7E1E2;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Yeseva One', cursive;
}

.app-wrapper {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  justify-content: space-between;
}

.main-content-wrapper {
  /*height: calc(100vh - 255px);*/
  height: 100%;
  max-width: 100vw;
  display: grid;
  grid-template-columns: 2fr 1.4fr 2fr;
  justify-content: center;
  background-image: url('./assets/content_background.svg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position-y: 13px;
  background-position-x: 5px;
  background-color: var(--color-blue-verylight);
}

.robo-arm-wrapper {
  display: flex;
  align-items: flex-end;
  justify-content: center;
  position: relative;
}

.robo-arm-wrapper > img {
  height: calc(100% - 70px);
  margin-bottom: -10px;
  position: absolute;
  left: -30px;
}

</style>
