<template>
  <div class="app-wrapper">
    <info-header :base-url="baseUrl"/>
    <div class="main-content-wrapper">
      <oven-block :status="left_oven" variant="left"/>
      <div class="robo-arm-wrapper">
        <img :src="robo_arm" alt="robotic arm image">
      </div>
      <oven-block :status="right_oven" variant="right"/>
    </div>
    <footer-links/>
  </div>
</template>

<script>
import axios from 'axios'

import InfoHeader from './components/Header'
import FooterLinks from './components/Footer'
import OvenBlock from './components/Oven'
// import StatusMessage from "@/components/StatusMessage";


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
      left_oven: 'available', //    4 states ->
      right_oven: 'available', // -> available, busy, cooking, finishing
      left_oven_baking_duration: '',
      left_oven_left: '',
      right_oven_baking_duration: '',
      right_oven_left: '',
      left_oven_status: true,
      right_oven_status: true,
      updateInterval: 1000,
      baseUrl: 'localhost:5000'
    }
  },
  methods: {
    getLeftOvenInfo(){
      axios.get(`http://${this.$data.baseUrl}/status-left`)
      .then(res => {
        if(res.status !== 200)
          console.log('Error requesting oven info')
        else {
          this.$data.left_oven = res.data.status // Reading oven status
          this.$data.left_oven_baking_duration = res.data.baking_duration // Reading baking duration
        }
      })
    },
    getRightOvenInfo(){
      axios.get(`http://${this.$data.baseUrl}/status-right`)
          .then(res => {
            if(res.status !== 200)
              console.log('Error requesting oven info')
            else {
              this.$data.right_oven = res.data.status // Reading oven status
              this.$data.right_oven_baking_duration = res.data.baking_duration // Reading baking duration
            }
          })
    },

    leftOvenWatcher(){
      switch(this.$data.left_oven){
        case 'cooking':
          if(!this.$data.left_oven_status) {
            this.$data.left_oven = true
            this.$data.left_oven_left = this.$data.left_oven_baking_duration
          } else {
            this.$data.left_oven_left = this.$data.left_oven_left - this.$data.updateInterval
            if(this.$data.left_oven_left <= 0) this.$data.left_oven_left = 0
          }
          break
        default:
          this.getLeftOvenInfo()
      }
    },
    rightOvenWatcher(){
      switch(this.$data.right_oven){
        case 'cooking':
          if(!this.$data.right_oven_status) {
            this.$data.right_oven = true
            this.$data.right_oven_left = this.$data.right_oven_baking_duration
          } else {
            this.$data.right_oven_left = this.$data.right_oven_left - this.$data.updateInterval
            if(this.$data.right_oven_left <= 0) this.$data.right_oven_left = 0
          }
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

      // this.$data.left_oven = !this.$data.left_oven
      // this.$data.right_oven = !this.$data.right_oven
    }, 10000)

  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Yeseva+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');
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
  font-size: 14px;
}

.app-wrapper {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  justify-content: space-between;
}

.main-content-wrapper {
  height: calc(100vh - 359px);
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
}

.robo-arm-wrapper > img {
  height: 550px;
  margin-bottom: -20px;
}


</style>
