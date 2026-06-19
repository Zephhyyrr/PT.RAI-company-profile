<template>
  <section id="home" class="hero section">
    <!-- Interactive CSS Background replacing header3.png -->
    <div class="hero-bg-custom">
      <div class="bg-top">
        <div class="hero-title-container">
          <h1 class="hero-company-title">{{ t.heroTitle }}</h1>
          <div class="hero-dots">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
          </div>
        </div>

        <!-- Decorative Leaves Left -->
        <div class="leaves-group leaves-left">
          <div class="leaf leaf-light"></div>
          <div class="leaf leaf-dark"></div>
        </div>

        <!-- Decorative Leaves Right -->
        <div class="leaves-group leaves-right">
          <div class="leaf leaf-light"></div>
          <div class="leaf leaf-dark"></div>
        </div>
      </div>
      <div class="bg-bottom"></div>
    </div>

    <div class="container text-center hero-content-wrapper">
      <!-- Carousel wrapper with Bootstrap classes -->
      <div id="carouselExample" class="carousel slide" data-bs-ride="carousel">
        <!-- Carousel Inner -->
        <div class="carousel-inner">
          <div
            v-for="(item, index) in items"
            :key="index"
            class="carousel-item"
            :class="{ active: index === 0 }"
          >
            <a :href="item.href" target="_blank" class="d-block w-100">
              <!-- Check if it's a YouTube link -->
              <template v-if="item.href">
                <!-- Embed YouTube video -->
                <iframe
                  :src="'https://www.youtube.com/embed/' + getYouTubeVideoId(item.href)"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                  class="d-block w-100 carousel-video"
                ></iframe>
              </template>
              <!-- If it's an image, display it -->
              <template v-else>
                <img
                  :src="item.src"
                  class="d-block w-100 rounded-lg carousel-image"
                  :alt="'Image ' + (index + 1)"
                />
              </template>
            </a>
          </div>
        </div>
        <!-- Carousel Controls -->
        <button
          class="carousel-control-prev"
          type="button"
          data-bs-target="#carouselExample"
          data-bs-slide="prev"
        >
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button
          class="carousel-control-next"
          type="button"
          data-bs-target="#carouselExample"
          data-bs-slide="next"
        >
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "HeroSection",
  data() {
    return {
      currentLang: "en",
      items: [
        { src: "assets/img/header/Owner-header.png" },
        { src: "/assets/img/images/cocofiber/cocofiber1.jpeg" },
        { src: "/assets/img/images/kayumanis-version/CinnamonStick-8cm.png" },
        { src: "/assets/img/images/kayumanis-version/Cinnamon-2.png" },
        { src: "/assets/img/images/kayumanis-version/Cinnamon-KF.png" },
        { src: "/assets/img/images/kayumanis-version/Cinnamon-KA/KB.png" },
        { href: "https://youtube.com/shorts/D0ukIEVJ5BQ?si=0zLi_6n0bOSETb2j" },
        { href: "https://youtube.com/shorts/hvtvDwcObiE?si=L5pZVeVQoksDrXRs" },
      ],
    };
  },
  computed: {
    t() {
      const isId = this.currentLang === "id";
      return {
        heroTitle: isId ? "Perusahaan Ekspor Kayu Manis" : "Cinnamon Export Company"
      };
    }
  },
  created() {
    this.currentLang = sessionStorage.getItem("app_lang") || localStorage.getItem("app_lang") || "en";
  },
  methods: {
    /**
     * Extract the YouTube video ID from a given URL.
     * Supports various YouTube URL formats, including `youtu.be`, `youtube.com/watch`,
     * `youtube.com/embed`, and `youtube.com/shorts`.
     *
     * @param {string} url - The YouTube URL.
     * @returns {string|null} - The extracted video ID or `null` if not found.
     */
    getYouTubeVideoId(url) {
      if (!url) return null;

      // Check for shorts URLs
      const shortUrlMatch = url.match(/youtube\.com\/shorts\/([a-zA-Z0-9_-]{11})/);
      if (shortUrlMatch) {
        return shortUrlMatch[1];
      }

      // Check for other YouTube formats
      const videoIdMatch = url.match(
        /(?:youtu\.be\/|youtube\.com\/(?:watch\?v=|embed\/|v\/|e\/|[^/]+\/[^/]+\/))([a-zA-Z0-9_-]{11})/
      );

      return videoIdMatch ? videoIdMatch[1] : null;
    },
  },
  mounted() {
    if (window.bootstrap) {
      const carouselElement = document.getElementById('carouselExample');
      if (carouselElement) {
        new window.bootstrap.Carousel(carouselElement, {
          interval: 3000,
          ride: 'carousel'
        });
      }
    }
  }
};
</script>


<style scoped src="./HeroSection.css"></style>
