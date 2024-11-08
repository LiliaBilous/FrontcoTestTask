<template>
  <div>
    <div class="carousel__image-container" v-for="(image, index) in images" :key="index">
      <img
        :src="image.url"
        @click="$emit('selectImage', image)"
        class="carousel__image"
        :class="{
          selected: selectedImages.includes(image),
        }"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: Array,
    selectedImages: Array,
  },
};
</script>
