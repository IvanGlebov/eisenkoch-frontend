<template>
  <div class="status-wrapper">
    <div class="status-content" :class="{'idle-wrapper': status === 'available'}"
    >
      {{ statusContent }}
    </div>
    <div class="status-message-corner" :class="{
          'left-corner': variant === 'left',
          'right-corner': variant === 'right',
          'idle-corner': status === 'available'
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
    status: String,
    timeLeft: Number
  },
  methods: {
    timeToString(number) {
      let minutes = number / 60
      let seconds = number % 60
      return minutes.toFixed(0) + ':' + ((seconds > 9) ? seconds : '0' + seconds)
    }
  },
  computed: {
    statusContent() {
      console.log('Status messaga')
      console.log(this)
      switch(this.status){
        case 'available':
          return 'Готов печь вафли'
        case 'busy':
          return 'Заливка теста'
        case 'cooking':
          return 'будут готовы через ' + this.timeToString(this.timeLeft)
        case 'finishing':
          return 'выгрузка'
        default:
          return 'Error'
      }
    }
  }
}
</script>

<style scoped>

.status-wrapper {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  width: 26vw;
  position: relative;
}

.status-content {
  background-color: var(--color-yellow);
  height: 7vh;
  font-family: 'Roboto Mono', monospace;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.3rem;
  font-weight: bold;
  text-transform: uppercase;
  color: var(--color-white);
  transition: all .5s;
}

.status-message-corner {
  position: absolute;
  height: 0;
  width: 0;
  left: calc(26vw - 7vh);
  top: calc(7vh - 1px);
}

.left-corner {
  border: 7vh solid transparent;
  border-right: 0;
  border-top: 7vh solid var(--color-yellow);
  transition: all .5s;
}

.right-corner {
  border: 7vh solid transparent;
  border-left: 0;
  border-top: 7vh solid var(--color-yellow);
  left: 0;
  transition: all .5s;
}

.idle-wrapper {
  background-color: var(--color-green);
  transition: all .5s;
}

.idle-corner {
  border-top: 7vh solid var(--color-green);
  transition: all .5s;
}

@media screen and (min-height: 900px) {
  .status-content {
    font-size: 2rem;
  }
}

</style>