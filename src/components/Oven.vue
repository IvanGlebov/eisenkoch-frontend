<template>
  <div class="waffle-wrapper" :class="{'left-wrapper': variant === 'left', 'right-wrapper': variant === 'right'}">
    <div class="status-message-wrapper">
      <status-message :variant="variant" :status="status" :time-left="timeLeft"/>
    </div>
    <div class="waffles-and-steam-wrapper">
      <img v-if="status !== 'available'" class="steam-icon" :src="steam" alt="steam image">
      <div class="waffles_icon-wrapper"
           :class="{'waffles_left_idle': variant === 'left' && status === 'available',
                    'waffles_right_idle': variant === 'right' && status === 'available'}">
        <img class="waffles_in_progress-icon" :src="waffles_in_progress" alt="waffles in progress image">
      </div>
      <img v-if="status !== 'available'" class="steam-icon" :src="steam" alt="steam image">
    </div>
    <img v-if="status !== 'available'" class="oven-image"
         :class="{'left-oven': variant === 'left', 'right-oven': variant === 'right' }"
         :src="oven_in_progress" alt="oven in progress image">
    <img v-if="status === 'available'" class="oven-image"
         :class="{'left-oven': variant === 'left', 'right-oven': variant === 'right' }"
         :src="oven_idle" alt="Oven idling image">
  </div>
</template>

<script>
import StatusMessage from './StatusMessage'

export default {
  name: "OvenBlock",
  props: {
    variant: String,
    status: String,
    timeLeft: String,
  },
  components: {
    StatusMessage
  },
  data() {
    return {
      oven_idle: require('../assets/oven_idle.svg'),
      oven_in_progress: require('../assets/oven_in_progress.svg'),
      steam: require('../assets/steam.svg'),
      waffles_idle: require('../assets/waffles_idle.svg'),
      waffles_in_progress: require('../assets/waffles_in_progress.svg'),
    }
  },
  computed: {
    wafflesStatus() {
      switch(this.status) {
        case 'available':
          return
      }
      return true
    }
  }
}
</script>

<style scoped>

.waffle-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: inherit;
}

.left-wrapper {
  align-items: flex-end;
}
.right-wrapper {
  align-items: flex-start;
}
.left-wrapper > .waffles-and-steam-wrapper {
  margin-right: 90px;
}
.right-wrapper > .waffles-and-steam-wrapper {
  margin-left: 60px;
}

.status-message-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-top: 106px;
}
.waffles-and-steam-wrapper {
  margin-right: 35px;
  height: 142px;
  display: flex;
  align-items: flex-end;
  margin-bottom: 28px;
  gap: 14px;
  position: relative;
}

.waffles-and-steam-wrapper > img {
  height: 100%;
}

.oven-image {
  width: 284px;
}
.oven-image.left-oven{
  margin-right: 89px;
}
.oven-image.right-oven  {
  margin-left: 65px;
}
.steam-icon {
  max-height: 63px;
  animation: 1.5s steam_cycle infinite linear;
}
.steam-icon:nth-child(1){
  transform: translateY(-30px);
  animation-delay: .75s;
}
.steam-icon:not(:nth-child(1)){
  transform: rotateY(180deg);
}


.waffles_icon-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 135px;
  width: 135px;
  border-radius: 50%;

  transition: all .5s;
}

.waffles_in_progress-icon {
  height: inherit;
}

.waffles_left_idle {
  position: absolute;
  background-color: var(--color-white);
  border-radius: 50%;
  width: 114px;
  height: 114px;
  padding: 21px;
  transform: translateY(20px) translateX(-230px);
  right: 10px;
  top: 0;
  transition: all .5s;
}

.waffles_right_idle {
  position: absolute;
  background-color: var(--color-white);
  border-radius: 50%;
  width: 114px;
  height: 114px;
  padding: 21px;

  left: 55px;
  top: 0;
  transform: translateY(20px) translateX(200px);

  transition: all .5s;
}



@keyframes steam_cycle {
  0% {
    opacity: 0;
    width: 63px;
    height: 0;
  }
  100%{
    opacity: 1;
    width: 63px;
    height: 63px;
  }
}


</style>