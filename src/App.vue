<template>
  <AppHeader />
  <div id="app">
    <router-view />
    <AppFooter />

    <div v-if="showLangPopup" class="lang-popup shadow-lg rounded">
      <button @click="dismissLangPopup" class="btn-close position-absolute"
        style="top: 15px; right: 15px; font-size: 12px;" aria-label="Close"></button>

      <div class="d-flex flex-column flex-sm-row align-items-start align-items-sm-center pe-4 gap-3">
        <div class="d-flex align-items-center">
          <i class="bi bi-globe fs-2 me-3 text-success"></i>
          <div class="d-flex flex-column" style="line-height: 1.2;">
            <span style="font-size: 15px; font-weight: bold; color: #333; margin-bottom: 3px;">Available in Another
              Language</span>
            <span style="font-size: 13px; color: #666;">Discover our site in your preferred language!</span>
          </div>
        </div>
        <div class="d-flex flex-column gap-2 mt-2 mt-sm-0 align-items-stretch w-100 w-sm-auto">
          <button @click="switchLanguageId" class="btn btn-sm btn-outline-success px-4 py-1 fw-bold"
            style="border-radius: 50px; font-size: 12px;">ID - Indonesia</button>
          <button @click="switchLanguageCn" class="btn btn-sm btn-outline-success px-4 py-1 fw-bold"
            style="border-radius: 50px; font-size: 12px;">CN - 中文</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AppFooter from "./components/AppFooter.vue";
import AppHeader from "./components/AppHeader.vue";
import AOS from 'aos';
import GLightbox from 'glightbox';
import Swiper from 'swiper';

export default {
  name: "App",
  components: {
    AppHeader,
    AppFooter,
  },
  data() {
    return {
      showLangPopup: false
    };
  },
  created() {
    if (!localStorage.getItem("app_lang_reset_v1")) {
      localStorage.removeItem("app_lang");
      localStorage.removeItem("lang_popup_seen");
      localStorage.setItem("app_lang_reset_v1", "true");
    }
  },
  methods: {
    aosInit() {
      AOS.init({
        duration: 600,
        easing: 'ease-in-out',
        once: true,
        mirror: false,
      });
    },
    initGlightbox() {
      GLightbox({
        selector: '.glightbox',
      });
    },
    initSwiper() {
      document.querySelectorAll(".init-swiper").forEach((swiperElement) => {
        const configElement = swiperElement.querySelector(".swiper-config");

        if (configElement) { // Check if .swiper-config exists
          const config = JSON.parse(configElement.innerHTML.trim());

          if (swiperElement.classList.contains("swiper-tab")) {
            this.initSwiperWithCustomPagination(swiperElement, config);
          } else {
            new Swiper(swiperElement, config);
          }
        } else {
          console.warn("Swiper config element not found for:", swiperElement);
        }
      });
    },

    initSwiperWithCustomPagination(swiperElement, config) {
      // Custom swiper initialization logic here if needed
      new Swiper(swiperElement, config);
    },
    handleHashScroll() {
      if (window.location.hash) {
        const section = document.querySelector(window.location.hash);
        if (section) {
          setTimeout(() => {
            const scrollMarginTop = getComputedStyle(section).scrollMarginTop;
            window.scrollTo({
              top: section.offsetTop - parseInt(scrollMarginTop),
              behavior: 'smooth',
            });
          }, 100);
        }
      }
    },
    dismissLangPopup() {
      this.showLangPopup = false;
      sessionStorage.setItem("lang_popup_seen", "true");
    },
    switchLanguageId() {
      localStorage.setItem("app_lang", "id");
      sessionStorage.setItem("lang_popup_seen", "true");
      window.location.reload();
    },
    switchLanguageCn() {
      localStorage.setItem("app_lang", "cn");
      sessionStorage.setItem("lang_popup_seen", "true");
      window.location.reload();
    }
  },
  mounted() {
    this.aosInit();
    this.initGlightbox();
    this.initSwiper();
    this.handleHashScroll();

    // Show language popup if applicable
    const currentLang = localStorage.getItem("app_lang") || "en";

    if (currentLang === "en") {
      setTimeout(() => {
        this.showLangPopup = true;
      }, 300); // reduced to 1s so it appears faster
    }

    window.addEventListener("load", this.handleHashScroll);
    window.addEventListener("load", this.initSwiper);
  },
};

</script>

<style>
.lang-popup {
  position: fixed;
  top: 90px;
  right: 20px;
  background: white;
  padding: 15px 20px;
  z-index: 9999;
  border-left: 5px solid #007a08;
  animation: slideDown 0.5s cubic-bezier(0.25, 0.8, 0.25, 1);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
}

@keyframes slideDown {
  from {
    transform: translateY(-50px);
    opacity: 0;
  }

  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@media (max-width: 576px) {
  .lang-popup {
    top: 70px;
    left: 15px;
    right: 15px;
    padding: 15px;
  }
}
</style>
