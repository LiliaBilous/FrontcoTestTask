<template>
  <div class="content__list">
    <h4 class="content__list-title">Selected Images:</h4>
    <ul class="content__list-body">
      <li class="content__list-item" v-for="(image, index) in images" :key="index">
        {{ image.url }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    images: Array,
  },
};
</script>
