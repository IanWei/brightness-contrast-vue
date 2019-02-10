<template>
    <div class="slider">
        <h3 class="slider__head">Filter</h3>
        <vue-slider></vue-slider>
        <p class="slider__content">Slide to adjust image filter type ! [icon] </p>
    </div>

</template>
<script>
    import vueSlider from 'vue-slider-component';
    export default {
      name: 'FilterSliderBar',
      components: {
        vueSlider
      }

    }
</script>
<style>

</style>