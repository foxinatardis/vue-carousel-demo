<template lang="html">
  <div class="carousel-component">
    <div class="outer-container">
      <div class="wrapper">
        <div v-for="(item, index) in items" :key="index">
          <div class="box" v-bind:class="{
            'far-left': (index === displayIndicies[0]),
            'left': (index === displayIndicies[1]),
            'center': (index === displayIndicies[2]),
            'right': (index === displayIndicies[3]),
            'far-right': (index === displayIndicies[4])
            }"
            :style="{'background-color': item.color}"
          >
          </div>
        </div>
      </div>
    </div>

    <div class="button-wrapper">
      <div class="left-clicker carousel-btn" v-on:click="moveCarousel('left')">
        <i class="fa fa-chevron-circle-left"></i>
      </div>
      <div class="right-clicker carousel-btn" v-on:click="moveCarousel('right')">
        <i class="fa fa-chevron-circle-right"></i>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      items: [
        { name: 'item 1', color: 'blue' },
        { name: 'item 2', color: 'red' },
        { name: 'item 3', color: 'green' },
        { name: 'item 4', color: 'pink' },
        { name: 'item 5', color: 'yellow' },
        { name: 'item 6', color: 'orange' }
      ],
      displayIndicies: []
    }
  },
  created () {
    for (let i = 0; i < this.items.length; i++) {
      this.displayIndicies.push(i)
    }
  },
  methods: {
    moveCarousel (direction) {
      if (direction === 'left') {
        this.displayIndicies.unshift(this.displayIndicies.pop())
      } else if (direction === 'right') {
        this.displayIndicies.push(this.displayIndicies.shift())
      }
    }
  }
}
</script>

<style lang="css">
  .outer-container {
    position: relative;
    height: 300px;
    clear: both;
    width: 0px;
    margin: 0 auto;
  }
  .wrapper {
    margin-left: -200px;
  }
  .box {
    position: absolute;
    background-color: grey;
    border: 1px solid black;
    height: 300px;
    width: 400px;
    z-index: -1;
    transition: transform 0.5s ease, z-index 0.2s linear;
    transform: perspective(200px) translateZ(-275px);
  }
  .far-left {
    transform: perspective(200px) translateZ(-175px) translateX(-47vw);
    z-index: 3;
  }
  .left {
    transform: perspective(200px) translateZ(-75px) translateX(-22vw);
    z-index: 5;
  }
  .center {
    transform: perspective(200px) translateZ(0px) translateX(0vw);
    z-index: 7;
  }
  .right {
    transform: perspective(200px) translateZ(-75px) translateX(22vw);
    z-index: 5;
  }
  .far-right {
    transform: perspective(200px) translateZ(-175px) translateX(47vw);
    z-index: 3;
  }
  .carousel-component {
    width: 100%;
    background-color: #eee;
    margin-bottom: 50px;
  }
  .button-wrapper {
    width: 0;
    margin: 0 auto;
    position: relative;
  }
  .carousel-btn {
    position: absolute;
    text-align: center;
    font-size: 50px;
    line-height: 50px;
    cursor: pointer;
  }
  .left-clicker {
    left: -75px;
  }
  .right-clicker {
    left: 25px;
  }
</style>
