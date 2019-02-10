<template>
    <div class="slider">
        <h3 class="slider__head" :style="{color: this.color}">{{ filter }}</h3>
        <vue-slider
                class="slider__bar"
                v-bind="options"
                v-model="sliderValue"
                @drag="adjust"
                ref="sliderRef"
                :disabled="!hasImage">
        </vue-slider>
        <p class="slider__content">Slide to adjust image {{ filter.toLowerCase() }} ! {{icon}} </p>
    </div>

</template>
<script>
    // Build a customised filter slider bar for different types of filter

    import vueSlider from 'vue-slider-component';
    import { EventBus } from "../event_bus";

    export default {
      name: 'FilterSliderBar',
      components: {
        vueSlider
      },
      props: {
        // change slider bar's color
        color: {
          type: String,
          required: true
        },
        // declare the type of filter
        filter: {
          type: String,
          required: true
        },
        icon: {
          type: String,
          required: true
        },
        // pass the name of event-listener
        sliderChange: {
          type: String,
          required: true
        },
        // enable the slider bar by conditional image
        hasImage: {
          type: Boolean,
          required: true
        }
      },
      data() {
        return {
          sliderValue: 0,
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
            min: -100,
            width: '94%',
            clickable: false
          }
        }
      },
      methods: {
        // emit the event listener to the App
        adjust() {
          // Update the canvas with the new data
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