<template>
    <div class="slider">
        <h3 class="slider__head" :style="{color: this.color}">{{ filter }}</h3>
        <vue-slider
                class="slider__bar"
                v-bind="options"
                v-model="sliderValue"
                @drag="adjust"
                ref="sliderRef">
        </vue-slider>
        <p class="slider__content">Slide to adjust image {{ filter.toLowerCase() }} ! {{icon}} </p>
    </div>

</template>
<script>
    import vueSlider from 'vue-slider-component';
    import { EventBus } from "../event_bus";

    export default {
      name: 'FilterSliderBar',
      components: {
        vueSlider
      },
      props: {
        color: {
          type: String,
          required: true
        },
        filter: {
          type: String,
          required: true
        },
        icon: {
          type: String,
          required: true
        },
        sliderChange: {
          type: String,
          required: true
        }
      },
      data() {
        return {
          sliderValue: 100,
          options: {
            tooltipStyle: {
              display: 'none'
            },
            sliderStyle: {
              backgroundColor: this.color
            },
            processStyle: {
              backgroundColor: this.color
            },
            width: '94%',
            clickable: false
          }
        }
      },
      methods: {
        adjust() {
          EventBus.$emit(this.sliderChange, this.$refs.sliderRef.value)
        }
      }
    }
</script>
<style>
    .slider {
        height: 9rem;
        margin: 0 2rem;
        border: 1px solid #eee;
        border-radius: 5px;
        box-shadow: 0 0 1rem .3rem #eee;
        margin-bottom: .5rem;
        text-align: center;
    }

    .slider__head {
        padding: 1.3rem 0;
        font-size: 1.3rem;
        font-weight: 400;
    }

    .slider__bar {
        margin: 0 auto .9rem auto;
    }

    .slider__content {
        font-weight: lighter;
        letter-spacing: .1rem;
    }
</style>