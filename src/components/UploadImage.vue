<template>
    <div class="container">
        <div class="container__image">
            <img src="" alt="image" ref="image">
        </div>
        <div class="tabs">
            <div class="tabs__box">
                <span class="tabx__box--name">NAME</span>
                <span class="tabx__box--attribute">file name</span>
            </div>
            <input type="file" class="tabs__upload" name="file" id="file" ref="file"/>
            <label for="file">UPLOAD</label>
        </div>
    </div>
</template>
<script>
    export default {
      name: 'UploadImage'
    }
</script>
<style>

</style>