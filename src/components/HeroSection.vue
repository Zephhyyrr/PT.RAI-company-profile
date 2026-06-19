<template>
  <section id="home" class="hero section">
    <div class="hero-bg">
      <img
        src="/assets/img/header/header3.png"
        alt="Background Image"
        class="w-full h-auto object-cover"
      />
    </div>
    <div class="container text-center mt-10">
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
};
</script>


<style scoped>
.hero {
  position: relative;
}

.hero-bg img {
  width: 100%;
  height: 900px; /* Tinggi background */
  object-fit: cover;
}

.carousel-inner {
  border-radius: 15px;
  overflow: hidden;
  margin-top: 20px; /* Geser carousel sedikit ke bawah */
}

.carousel-item img {
  object-fit: cover;
  border-radius: 15px;
  height: 400px; /* Tinggi default untuk desktop */
}

/* Responsiveness for Carousel */
.carousel-image {
  width: 100%;
  height: auto;
  object-fit: cover;
  border-radius: 15px;
}

.carousel-video {
  width: 100%;
  height: 400px;
  border-radius: 15px;
}

/* Maintain aspect ratio in mobile */
@media (max-width: 768px) {
  .carousel-item img,
  .carousel-video {
    height: auto; /* Buat tinggi mengikuti lebar untuk menjaga proporsi */
    aspect-ratio: 16 / 9; /* Rasio video */
    max-height: 300px; /* Maksimal tinggi di layar kecil */
  }
}

button.carousel-control-prev,
button.carousel-control-next {
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  height: 50px;
  width: 50px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  align-items: center;
  justify-content: center;
}

button.carousel-control-prev {
  left: 10px;
}

button.carousel-control-next {
  right: 10px;
}

button.carousel-control-prev:hover,
button.carousel-control-next:hover {
  background-color: rgba(0, 0, 0, 0.7);
}
</style>
