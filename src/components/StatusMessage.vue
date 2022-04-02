<template>
  <div class="status-wrapper">
    <div class="status-content" :class="{'idle-wrapper': status}">{{ status ? 'Готов печь вафли' : 'будет готово через ' + timeToString(timeLeft) }}</div>
    <div class="status-message-corner" :class="{
          'left-corner': variant === 'left',
          'right-corner': variant === 'right',
          'idle-corner': status
    }"></div>
  </div>
</template>

<script>
export default {
  name: "StatusMessage",
  props: {
    variant: {
      type: String,
      validator: function (prop) {
        return (prop === 'left' || prop === 'right')
      }
    },
    status: Boolean,
    timeLeft: Number
  },
  methods: {
    timeToString(number) {
      let minutes = number / 60
      let seconds = number % 60
      return minutes.toFixed(0) + ':' + ((seconds > 9) ? seconds : '0' + seconds)
    }
  }
}
</script>

<style scoped>

.status-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  width: 570px;
  position: relative;
}

.status-content {
  background-color: var(--color-yellow);
  height: 81px;
  font-family: 'Roboto Mono', monospace;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.8rem;
  text-transform: uppercase;
  color: var(--color-white);
  transition: all .5s;
}

.status-message-corner {
  position: absolute;
  height: 0;
  width: 0;
  left: 490px;
  top: 79px;
}

.left-corner {
  border: 80px solid transparent;
  border-right: 0;
  border-top: 80px solid var(--color-yellow);
  transition: all .5s;
}

.right-corner {
  border: 80px solid transparent;
  border-left: 0;
  border-top: 80px solid var(--color-yellow);
  left: 0;
  transition: all .5s;
}

.idle-wrapper {
  background-color: var(--color-green);
  transition: all .5s;
}

.idle-corner {
  border-top: 80px solid var(--color-green);
  transition: all .5s;
}

</style>