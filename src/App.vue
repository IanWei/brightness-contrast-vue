<template>
    <div id="app">
        <header class="title">
            <h2 class="title__head">Brightness & Contrast Developer Test</h2>
            <p class="title__content">08 Feb, 2019 ー 15 Feb, 2019</p>
        </header>
        <div class="image-box">
            <img src="./assets/hero.png" alt="hero">
        </div>
        <div class="profile">
            <img src="./assets/ian.png" alt="Ian" class="profile-image">
        </div>
        <FilterSliderBar
                color="#26A95B"
                filter="Brightness"
                icon="☀️"
                sliderChange="bright-change"
                :hasImage="hasImage">
        </FilterSliderBar>
        <FilterSliderBar
                color="#4A90E2"
                filter="Contrast"
                icon="🌓"
                sliderChange="contrast-change"
                :hasImage="hasImage">
        </FilterSliderBar>
        <UploadImage></UploadImage>
    </div>
</template>

<script>

  import FilterSliderBar from './components/FilterSliderBar';
  import UploadImage from './components/UploadImage';
  import { EventBus } from "./event_bus";

  function applyContrast(data, contrast) {
    var factor = (259.0 * (contrast + 255.0)) / (255.0 * (259.0 - contrast));
    for (var i = 0; i < data.length; i+= 4) {
      data[i] = truncateColor(factor * (data[i] - 128.0) + 128.0);
      data[i+1] = truncateColor(factor * (data[i+1] - 128.0) + 128.0);
      data[i+2] = truncateColor(factor * (data[i+2] - 128.0) + 128.0);
    }
  }

  function truncateColor(value) {
    if (value < 0) {
      value = 0;
    } else if (value > 255) {
      value = 255;
    }
    return value;
  }

  function applyBrightness(data, brightness) {
    for (var i = 0; i < data.length; i+= 4) {
      data[i] += 255 * (brightness / 100);
      data[i+1] += 255 * (brightness / 100);
      data[i+2] += 255 * (brightness / 100);
    }
  }

  export default {
    name: 'app',
    components: {
      FilterSliderBar,
      UploadImage
    },
    data() {
      return {
        hasImage: false,
        drawnImage: null
      }
    },
    methods: {
      applyFilter(applyFunc, value) {
        const canvas = document.querySelector('#canvas');
        const ctx = canvas.getContext('2d');
        let ratio = canvas.width / this.drawnImage.width; // Every time should reset the data value
        canvas.height = this.drawnImage.height * ratio;
        ctx.drawImage(this.drawnImage, 0, 0, this.drawnImage.width, this.drawnImage.height, 0, 0, canvas.width, canvas.height);
        const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
        applyFunc(imageData.data, value);
        ctx.putImageData(imageData, 0, 0);
      }
    },
    mounted() {
      // Listen slider bar change event
      EventBus.$on('bright-change', (value) => {
        this.applyFilter(applyBrightness, value);
      });
      EventBus.$on('contrast-change', (value) => {
        this.applyFilter(applyContrast, value);
      });

      // Listen uploading image event
      EventBus.$on('get-image', (value) => {
        this.hasImage = value;
      });
      EventBus.$on('set-image', value => {
        this.drawnImage = value;
      })
    }
  }
</script>

<style>
    /************/
    /*Base Style*/
    /************/

    *,
    *::before,
    *::after {
        box-sizing: inherit;
        padding: 0;
        margin: 0;
    }

    html {
        font-size: 62.5%;
    }

    body {
        box-sizing: border-box;
        font-family: sans-serif;
        font-weight: normal;
        font-size: 1rem;
        line-height: 1;
        background-color: #ECECEC;
    }

    #app {
        width: 37.5rem;
        margin: 0 auto;
        background-color: #fff;
        padding-bottom: 1rem;
    }

    /*Title*/

    .title {
        width: 100%;
        height: 7rem;
        color: #fff;
        background-color: #7045B9;
        text-align: center;
    }

    .title__head {
        padding-top: 2rem;
        padding-bottom: 1rem;
    }

    .title__content {
        font-size: .9rem;
        font-weight: 300;
        letter-spacing: .1rem;
    }

    .image-box {
        margin-bottom: 2rem;
    }

    img {
        width: 100%;
        margin: 0 auto;
        display: inline-block;
    }

    .profile {
        width: 7rem;
        height: 7rem;
        border: 2px solid #fff;
        border-radius: 50%;
        margin: -7rem auto 1rem auto;
        overflow: hidden;
    }

    .profile-image {
        background-repeat: no-repeat;
        background-size: cover;
        width: 6.5rem;
        height: 6.5rem;
        border-radius: 50%;
        border: 2px solid #fff;
    }
</style>
