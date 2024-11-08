<template>
  <div class="content__image-container">
    <img
      v-for="(image, index) in images"
      :key="index"
      :src="image.url"
      @click="$emit('selectImage', image)"
      class="content__image"
      :class="{ selected: selectedImages.includes(image) }"
    />
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
