<template>
  <div class="waffle-wrapper" :class="{'left-wrapper': variant === 'left', 'right-wrapper': variant === 'right'}">
    <div class="status-message-wrapper">
      <status-message :variant="variant" :status="status" :time-left="123"/>
    </div>
    <div class="waffles-and-steam-wrapper">
      <img v-if="!status" class="steam-icon" :src="steam" alt="steam image">
      <div class="waffles_icon-wrapper"
           :class="{'waffles_left_idle': variant === 'left' && status,
                    'waffles_right_idle': variant === 'right' && status}">
        <img class="waffles_in_progress-icon" :src="waffles_in_progress" alt="waffles in progress image">
      </div>
      <img v-if="!status" class="steam-icon" :src="steam" alt="steam image">
    </div>
    <img v-if="!status" class="oven-image"
         :class="{'left-oven': variant === 'left', 'right-oven': variant === 'right' }"
         :src="oven_in_progress" alt="oven in progress image">
    <img v-if="status" class="oven-image"
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
    status: Boolean
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
.status-message-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-top: 150px;
}
.waffles-and-steam-wrapper {
  margin-right: 85px;
  height: 200px;
  display: flex;
  align-items: flex-end;
  margin-bottom: 40px;
  gap: 20px;
  position: relative;
}

.waffles-and-steam-wrapper > img {
  height: 100%;
}

.oven-image {
  width: 400px;
}
.oven-image.left-oven{
  margin-right: 125px;
}
.oven-image.right-oven  {
  margin-left: 50px;
}
.steam-icon {
  max-height: 125px;
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
  height: 190px;
  width: 190px;
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
  width: 160px;
  height: 160px;
  padding: 30px;
  transform: translateY(20px) translateX(-240px);
  right: 100px;
  top: 40px;
  transition: all .5s;
}

.waffles_right_idle {
  position: absolute;
  background-color: var(--color-white);
  border-radius: 50%;
  width: 160px;
  height: 160px;
  padding: 30px;

  left: 150px;
  top: 40px;
  transform: translateY(20px) translateX(220px);

  transition: all .5s;
}

/*.waffles_idle_right-icon {*/
/*  position: absolute;*/
/*  left: 370px;*/
/*  top: 70px;*/
/*  height: 170px !important;*/
/*}*/

/*.waffles_idle_left-icon {*/
/*  position: absolute;*/
/*  height: 170px !important;*/
/*  right: 360px;*/
/*  top: 70px;*/
/*}*/



@keyframes steam_cycle {
  0% {
    /*transform: scale(0);*/
    opacity: 0;
    width: 128px;
    height: 0;
  }
  100%{
    /*transform: scale(1);*/
    opacity: 1;
    width: 128px;
    height: 125px;
  }

}


</style>