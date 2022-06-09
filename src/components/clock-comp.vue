<template>
  <div class="clock" :style="{'--color': clockColor}">
    <svg>
      <circle class="outer" cx="95" cy="95" r="95"></circle>
      <circle class="inner" cx="95" cy="95" r="95" :stroke-dashoffset="Math.floor(697 - rotate * (597 / 360))"></circle>
    </svg>
    <div class="timer" :style="{'color': clockColor}">{{Math.floor(rotate / 6)}} 
      <br>
      {{(dataType === 'seconds') ? 'seconds' : (dataType === 'mins') ? 'mins' : 'hours'}}
    </div>
    <div class="dot" :style="{'transform': `rotate(${rotate}deg)`}"></div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  name: 'clock-comp',
  data() {
    return {
      rotate: 0 as number
    }
  },
  props: {
    clockColor: {
      type: String,
      default: '#54f757'
    },
    dataType: {
      type: String,
      default: 'seconds'
    }
  },
  computed: {
    time(): number {
      return (this.dataType === 'seconds') ? 100 : (this.dataType === 'mins') ? 100 * 60 : 100 * 60 * 60
    }
  },
  methods: {
    count() {
      this.rotate = (this.rotate === 360) ? 0 : this.rotate += 1
    },
  },
  mounted() {
    setInterval(() => {
      this.count()
    }, Math.floor(this.time))
  }
})
</script>

<style lang="scss" scoped>
  @keyframes glow {
    0% {
      box-shadow: 0px 0px 10px 5px var(--color);
    }

    100% {
      box-shadow: 0px 0px 15px 5px var(--color);
    }
  }

  .clock {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    // margin: 0 auto;
    width: 200px;
    height: 200px;
    border-radius: 50%;
  }

  .clock svg {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    transform: rotate(270deg);
  }

  .clock .outer {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -2;
    fill: transparent;
    stroke: #1a1919;
    stroke-width: 5px;
    transform: translate(5px, 5px);
  }

  .clock .inner {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    fill: transparent;
    stroke: var(--color);
    stroke-width: 5px;
    stroke-dasharray: 697;
    transform: translate(5px, 5px);
  }

  .timer {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 20px;
    line-height: 24px;
    z-index: 1;
  }

  .dot {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    height: 100%;

    &:after {
      content: "";
      position: absolute;
      width: 15px;
      height: 15px;
      background-color: var(--color);
      border-radius: 50%;
      transform: translate(calc(-50% + 5px), calc(-50% + 5px));
      animation: glow .5s linear infinite alternate;
    }
  }
</style>