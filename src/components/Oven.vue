<template>
  <div class="waffle-wrapper" :class="{'left-wrapper': variant === 'left', 'right-wrapper': variant === 'right'}">
    <div class="status-message-wrapper">
      <status-message :variant="variant" :status="status" :time-left="timeLeft"/>
    </div>
    <div class="oven-and-waffles-wrapper">
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

.oven-and-waffles-wrapper {
  position: relative;
  display: flex;
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
  margin-top: 80px;
}
.waffles-and-steam-wrapper {
  height: 9vw;
  display: flex;
  gap: 14px;
  bottom: 30vh;
  position: absolute;
}

.left-wrapper .waffles-and-steam-wrapper {
  align-items: center;
}

.right-wrapper .waffles-and-steam-wrapper {
  margin-left: 4.5vw;
  align-items: center;
}

.waffles-and-steam-wrapper > img {
  height: 100%;
}

.oven-image {
  /*width: 284px;*/
  width: 22vw;
}
.oven-image.left-oven{
  margin-right: 89px;
}
.oven-image.right-oven  {
  margin-left: 65px;
}
.steam-icon {
  max-height: 6vw;
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
  height: 9vw;
  width: 9vw;
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
  /*width: 114px;*/
  width: 7vw;
  /*height: 114px;*/
  height: 7vw;
  /*padding: 21px;*/
  padding: 1.5vw;

  /*transform: translateY(20px) translateX(-230px);*/
  /*left: 140px;*/
  /*top: -10px;*/
  left: 6vw;
  top: -1vh;
  transform: translateY(4.5vh) translateX(-11.5vw);

  transition: all .5s;
}

.right-wrapper .waffles_icon-wrapper {
  transform: rotateY(180deg);
}

.waffles_right_idle {
  position: absolute;
  background-color: var(--color-white);
  border-radius: 50%;
  /*width: 114px;*/
  width: 7vw;
  /*height: 114px;*/
  height: 7vw;
  /*padding: 21px;*/
  padding: 1.5vw;

  /*left: 55px;*/
  /*top: 0;*/
  left: 5vw;
  top: -1vh;
  transform: translateY(4vh) translateX(11vw) rotateY(180deg) !important;
  /*transform: rotateY(180deg) !important;*/
  transition: all .5s;
}



@keyframes steam_cycle {
  0% {
    opacity: 0;
    width: 6vw;
    height: 0;
  }
  100%{
    opacity: 1;
    width: 6vw;
    height: 6vw;
  }
}


</style>