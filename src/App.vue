<script>
import Carousel from "./components/CarouselWrap.vue";
import ListSelectedImages from "./components/ListSelectedImages.vue";

export default {
  components: {
    Carousel,
    ListSelectedImages,
  },
  data() {
    return {
      images: [],
      selectedImages: [],
    };
  },
  methods: {
    async fetchImages() {
      try {
        const response = await fetch("https://picsum.photos/v2/list");
        const data = await response.json();

        this.images = data.map((img) => ({
          url: `https://picsum.photos/id/${img.id}/600/400`,
        }));
      } catch (error) {
        console.error("Помилка при завантаженні зображень:", error);
      }
    },
    updateSelectedImages(selected) {
      this.selectedImages = selected;
    },
  },
  mounted() {
    this.fetchImages();
  },
};
</script>

<template>
  <div class="wrapper">
    <header class="header">
      <p>Fronted test task from Frontco</p>
    </header>

    <main class="content">
      <Carousel
        :images="images"
        :selectedImages="selectedImages"
        @updateSelectedImages="updateSelectedImages"
      />
      <ListSelectedImages :images="selectedImages" />
    </main>
    <footer class="footer">
      <div>
        Made by
        <a class="footer__copyright" href="https://github.com/LiliaBilous" target="_blank"
          >LiliiaBilous</a
        >
        in 2024
      </div>
    </footer>
  </div>
</template>
