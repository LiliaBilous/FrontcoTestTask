<template>
  <div class="content__carousel">
    <CarouselItem
      class="carousel"
      :images="visibleImages"
      @selectImage="selectImage"
      :selectedImages="selectedImages"
    ></CarouselItem>
    <div class="carousel__nav-buttons">
      <button class="carousel__button" @click="prevImage">
        <span>&#10094;</span>
        Prev
      </button>
      <button class="carousel__button" @click="nextImage">
        Next <span>&#10095;</span>
      </button>
    </div>
  </div>
</template>

<script>
import CarouselItem from "./CarouselItem.vue";
export default {
  components: {
    CarouselItem,
  },
  props: {
    images: {
      type: Array,
      required: true,
    },
    selectedImages: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      currentIndex: 0,
      imagesPerView: 1,
    };
  },
  computed: {
    visibleImages() {
      const totalImages = this.images.length;

      if (this.currentIndex + this.imagesPerView <= totalImages) {
        return this.images.slice(
          this.currentIndex,
          this.currentIndex + this.imagesPerView
        );
      } else {
        const endPart = this.images.slice(this.currentIndex);
        const startPart = this.images.slice(0, this.imagesPerView - endPart.length);
        return [...endPart, ...startPart];
      }
    },
  },
  methods: {
    updateImagesPerView() {
      const containerWidth = window.innerWidth;
      if (containerWidth > 1200) {
        this.imagesPerView = 5;
      } else if (containerWidth > 768) {
        this.imagesPerView = 3;
      } else {
        this.imagesPerView = 1;
      }
    },

    nextImage() {
      this.currentIndex = (this.currentIndex + 1) % this.images.length;
    },
    prevImage() {
      this.currentIndex =
        (this.currentIndex - 1 + this.images.length) % this.images.length;
    },
    selectImage(image) {
      const updatedSelectedImages = [...this.selectedImages];
      const imageIndex = updatedSelectedImages.indexOf(image);

      if (imageIndex > -1) {
        updatedSelectedImages.splice(imageIndex, 1);
      } else {
        updatedSelectedImages.push(image);
      }

      this.$emit("updateSelectedImages", updatedSelectedImages);
    },
  },
  mounted() {
    this.updateImagesPerView();
    window.addEventListener("resize", this.updateImagesPerView);
  },
  beforeUnmount() {
    window.removeEventListener("resize", this.updateImagesPerView);
  },
};
</script>
