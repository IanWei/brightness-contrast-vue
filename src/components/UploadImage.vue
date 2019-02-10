<template>
    <div class="container">
        <div class="container__image">
            <p v-if="!hasImage">Please Upload your image</p>
            <img src="" :style="filter" alt="image" ref="image" :class="{ hide: hasImage === false }">
        </div>
        <div class="tabs">
            <div class="tabs__box">
                <span class="tabs__box--name">NAME</span>
                <span class="tabs__box--attribute">{{ filename }}</span>
            </div>
            <input type="file" class="tabs__upload" name="file" id="file" ref="file" @change="uploadImage"/>
            <label for="file">UPLOAD</label>
        </div>
    </div>
</template>
<script>
    import { EventBus } from "../event_bus";

    export default {
      name: 'UploadImage',
      props: {
        brightnessValue: {
          type: Number,
          required: true
        },
        contrastValue: {
          type: Number,
          required: true
        }
      },
      data() {
        return {
          filename: 'A LONG FILE NAME …',
          hasImage: false
        }
      },
      methods: {
        // Upload the image from the local computer, and render the truncated filename

        uploadImage() {
          const preview = this.$refs.image;
          const file = this.$refs.file.files[0];
          let name = '';
          const reader = new FileReader();
          reader.onload = function() {
            preview.src = reader.result;
          };
          if (file) {
            this.hasImage = true;
            reader.readAsDataURL(file);
            name = file.name;
            if (name.length > 14) {
              this.filename = name.slice(0, 18).concat(' ...');
            } else {
              this.filename = name;
            }
          } else {
            this.hasImage = false;
            this.filename = 'A LONG FILE NAME …';
            preview.src = "";
          }

          EventBus.$emit('get-image', this.hasImage);
        }
      },
      computed: {
        // render filtered image synchronously
        filter() {
          return { filter: `brightness(${this.brightnessValue}%) contrast(${this.contrastValue}%)`}
        }
      }
    }

</script>
<style>
    .container {
        border-radius: 5px;
        margin: 2rem;
        border: 1px solid #DCDEE4;
        overflow: hidden;
    }

    .container__image {
        margin-bottom: 1rem;
        max-height: 21rem;
        width: 33.3rem;
        height: auto;
        overflow: hidden;
    }

    .tabs {
        padding: 0 .6rem;
        margin-bottom: .6rem;
        font-weight: 600;
        letter-spacing: 1px;
    }

    .tabs__box {
        display: inline-block;
        border: 1px solid #E9EBEE;
        border-radius: 5px;
        text-align: center;
    }
    .tabs__box span {
        padding: 1rem;
        display: inline-block;
    }

    .tabs__box--name {
        color: #8392A6;
        width: 6rem;
        background-color: #F6F8FA;
    }

    .tabs__box--attribute {
        color: #4BB775;
        border-left: 1px solid #E9EBEE;
        width: 15rem;
    }

    .tabs__upload {
        opacity: 0;
        width: 0.1px;
        height: 0.1px;
        overflow: hidden;
        position: absolute;
        z-index: -1;
    }

    .tabs__upload + label {
        color: #4A90E2;
        display: inline-block;
        float: right;
        padding: 1rem .8rem;
        border-radius: 5px;
        border: 1px solid #E9EBEE;
        width: 8.5rem;
        text-align: center;
        font-weight: 600;
        position: relative;
        padding-left: 2.6rem;
        background-color: #F6F8FA;
    }

    .tabs__upload + label::before {
        content: '';
        position: absolute;
        width: 0;
        height: 0;
        left: 1rem;
        top: 1.2rem;
        border-left: .5rem solid transparent;
        border-right: .5rem solid transparent;
        border-bottom: .7rem solid #4A90E2;
    }

    .tabs__upload:focus + label,
    .tabs__upload + label:hover,
    .tabs__upload + label:active {
        background-color: #eee;
    }
    .tabs__upload + label {
        cursor: pointer;
    }

    /*hide the image icon if there is no image*/
    .hide {
        opacity: 0;
    }
</style>