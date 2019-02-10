<template>
    <div id="app">
        <header class="title">
            <h2 class="title__head">Brightness & Contrast Developer Test</h2>
            <p class="title__content">08 Feb, 2019 - 15 Feb, 2019</p>
        </header>
        <div class="image-box">
            <img src="./assets/hero.png" alt="hero">
        </div>
        <div class="profile">
            <img src="./assets/ian.png" alt="Ian">
        </div>
        <FilterSliderBar></FilterSliderBar>
    </div>
</template>

<script>


  import FilterSliderBar from './components/FilterSliderBar';

  export default {
    name: 'app',
    components: {
      FilterSliderBar
    }
  }
</script>

<style>
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

    .title {
        width: 100%;
        height: 7rem;
        color: #fff;
        background-color: #7045B9;
        text-align: center;
        letter-spacing: .2rem;
    }

    .title__head {
        padding-top: 2rem;
        padding-bottom: 1rem;
    }

    .title__content {
        font-size: .9rem;
        font-weight: 300;
    }

    .image-box {
        margin-bottom: 2rem;
    }

    img {
        width: 100%;
    }

    .profile {
        width: 6.5rem;
        height: 6.5rem;
        border: 2px solid #fff;
        border-radius: 50%;
        margin: -7rem auto 1rem auto;
        overflow: auto;
    }
</style>
