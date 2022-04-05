<template>
  <div class="header">
    <div class="tokens-wrapper">
      <div class="tokens-earned-header">Заработал токенов:</div>
      <div class="tokens-earned-content">{{ tokensEarned !== '' ? tokensEarned : '***,**' }}</div>
    </div>
    <div class="header-title">
      робот, который печёт вафли
    </div>
    <div class="waffles-wrapper">
      <div class="waffles-baked-header">{{ (wafflesBaked !== 'waiting' && wafflesBaked !== '') ? 'всего испёк вафель' : 'Загрузка робота'}}</div>
      <div class="waffles-baked-content">{{ (wafflesBaked !== 'waiting' && wafflesBaked !== '') ? wafflesBaked : '***'}}</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: "InfoHeader",
  data() {
    return {
      baseUrl: 'localhost:5002',
      wafflesBaked: '',
      tokensEarned: ''
    }
  },
  methods: {
    getWafflesInfo() {
      axios.get(`http://${this.$data.baseUrl}/total-waffles`)
      .then(res => {
        if(res.status !== 200)
          console.log('Error reading waffles amount')
        else {
          this.$data.wafflesBaked = res.data.status // Reading waffles amount status
        }
      })
    },
    getTokensInfo() {
      axios.get(`http://${this.$data.baseUrl}/update-balance`)
      .then(res => {
        if(res.status !== 200)
          console.log('Error reading balance')
        else {
          this.tokensEarned = res.data.balance // Reading balance of robot
        }
      })
    }
  },
  mounted() {
    this.getWafflesInfo()
    this.getTokensInfo()
    setInterval(() => {
      this.getWafflesInfo()
      this.getTokensInfo()
    }, 30000)
  }
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