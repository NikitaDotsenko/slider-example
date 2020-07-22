<template>
  <div id="app">
    <div class="wrapper" v-for="(image, key) in imagesCollection" :key="key" :class="{'active': key===currentImageIndex && currentImageIndex!==0}">
      <div class="background" :style="{'--bkgImage': 'url(' + image + ')', '--bkgImageMobile': 'url(' + image + ')'}"></div>
      <div class="img-content">
        <img :src="image">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'App',
    components: {},
    props: {
      interval: {
        type: Number,
        default: 2000
      },
      animationStyle: {
        type: String,
        default: 'box'
      },
      animationCurve: {
        type:String,
        default: 'linear'
      },
      animationLoop: {
        type: String,
        default: 'infinite'
      }
    },
    data () {
      return {
        currentImageIndex:0
      }
    },
    computed: {
      imagesCollection() {
        return [
          'covers/xx.png',
          'covers/astroworld.jpeg',
          'covers/discogs.jpeg',
          'covers/syre.jpeg',
          'covers/mars.jpeg',
          'covers/xx.png',
        ];
      },
    },
    mounted() {
     setInterval(() => this.swapImage(), this.interval)
    },
    methods: {
      swapImage () {
        this.currentImageIndex += 1
        if (this.currentImageIndex === this.imagesCollection.length){
          this.currentImageIndex = 1
        }
      }
    }
  };
</script>

<style scoped>
  .wrapper {
    display: flex;
    width: 100%;
    height: 100vh;
    align-items: center;
    justify-content: center;
    position: absolute;
    left: 0;
    top: 0;
  }
  .active {
    z-index: 4;
    animation: box 2s infinite linear;
    position: relative;
  }
  .background {
    background-image: var(--bkgImage);
    background-repeat: no-repeat;
    background-size: cover;
    filter: blur(1.5rem);
    width: 100%;
    height: 100%;
    position: absolute;
  }

  .img-content {
    position: relative;
    width: 400px;
    height: 400px;
    z-index: 1;
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }

  @keyframes box {
    from { z-index: 2; opacity: 0.1; }
    to { z-index: 4; opacity: 1; }
  }
</style>
