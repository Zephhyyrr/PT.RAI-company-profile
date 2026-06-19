<template>
  <header id="header" class="header d-flex align-items-center fixed-top">
    <div
      class="container-fluid container-xl position-relative d-flex align-items-center"
    >
      <router-link to="/" class="logo d-flex align-items-center me-auto">
        <img src="/assets/img/logo/favicon.png" alt="Rumpun Alam Indonesia Logo" class="img-fluid" />
        <h1 class="sitename">Rumpun Alam Indonesia</h1>
      </router-link>

      <nav id="navmenu" class="navmenu fs-5">
        <ul>
          <li>
            <router-link
              to="/"
              :class="{ active: isActive('home') }"
              @click.prevent="scrollTo('home')"
              >Home</router-link
            >
          </li>
          <li>
            <router-link
              to="#"
              :class="{ active: isActive('about') }"
              @click.prevent="scrollTo('about')"
              >About</router-link
            >
          </li>
          <li class="dropdown">
            <router-link
              to="#"
              :class="{ active: isActive('product') }"
              @click.prevent="scrollTo('product')"
            >
              {{ t().products }}
              <i class="bi bi-chevron-down toggle-dropdown"></i>
            </router-link>
            <ul>
              <li v-for="value in products" :key="value.id">
                <router-link :to="{ path: '/product/' + value.id }">
                  {{ value.title }}
                </router-link>
              </li>
            </ul>
          </li>
          <!-- <li>
            <router-link
              to="#"
              :class="{ active: isActive('organization') }"
              @click.prevent="scrollTo('organization')"
              >Organization</router-link
            >
          </li> -->
          <li>
            <router-link
              to="#"
              :class="{ active: isActive('contact') }"
              @click.prevent="scrollTo('contact')"
              >Contact</router-link
            >
          </li>
          <li style="margin-left: 20px; display: flex; gap: 10px; align-items: center; justify-content: center;">
            <a href="#" @click.prevent="setLanguage('id')" :style="{ opacity: currentLang === 'id' ? 1 : 0.4 }" style="padding: 0; text-decoration: none; transition: 0.3s;" title="Indonesia">
              <img src="https://flagcdn.com/w40/id.png" width="24" alt="Indonesia" style="border-radius: 3px; box-shadow: 0 1px 2px rgba(0,0,0,0.2);">
            </a>
            <a href="#" @click.prevent="setLanguage('en')" :style="{ opacity: currentLang === 'en' ? 1 : 0.4 }" style="padding: 0; text-decoration: none; transition: 0.3s;" title="English">
              <img src="https://flagcdn.com/w40/gb.png" width="24" alt="English" style="border-radius: 3px; box-shadow: 0 1px 2px rgba(0,0,0,0.2);">
            </a>
            <a href="#" @click.prevent="setLanguage('cn')" :style="{ opacity: currentLang === 'cn' ? 1 : 0.4 }" style="padding: 0; text-decoration: none; transition: 0.3s;" title="中文">
              <img src="https://flagcdn.com/w40/cn.png" width="24" alt="中文" style="border-radius: 3px; box-shadow: 0 1px 2px rgba(0,0,0,0.2);">
            </a>
          </li>
        </ul>
        <i
          class="mobile-nav-toggle d-xl-none bi bi-list"
          @click="toggleMobileMenu"
        ></i>
      </nav>
    </div>
  </header>
</template>

<script>
import productsEn from "../data/products-en.json";
import productsId from "../data/products-id.json";
import productsCn from "../data/products-cn.json";
import AOS from "aos";
import "aos/dist/aos.css";

export default {
  name: "AppHeader",
  data() {
    return {
      products: [],
      activeSection: "home",
      currentLang: "en"
    };
  },
  created() {
    this.currentLang = localStorage.getItem("app_lang") || "en";
    let allProducts = productsEn;
    if (this.currentLang === "id") allProducts = productsId;
    if (this.currentLang === "cn") allProducts = productsCn;
    this.products = allProducts.filter(p => p.id !== "cardamom");
  },
  mounted() {
    AOS.init();
    window.addEventListener("scroll", this.handleScroll);

    this.setActiveSectionOnRoute();
  },
  beforeUnmount() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  watch: {
    $route() {
      this.setActiveSectionOnRoute();
    },
  },
  methods: {
    t() {
      const isId = this.currentLang === "id";
      const isCn = this.currentLang === "cn";
      return {
        products: isId ? "Produk" : isCn ? "产品" : "Products"
      };
    },
    scrollTo(sectionId) {
      if (this.$route.path.includes("/product/")) {
        // Redirect to home page and scroll after navigation
        this.$router.push("/").then(() => {
          this.setActive(sectionId);
          this.$nextTick(() => {
            const element = document.getElementById(sectionId);
            if (element) {
              element.scrollIntoView({ behavior: "smooth" });
            }
          });
        });
      } else {
        // Just scroll on the current page
        this.setActive(sectionId);
        this.$nextTick(() => {
          const element = document.getElementById(sectionId);
          if (element) {
            element.scrollIntoView({ behavior: "smooth" });
          }
        });
      }
    },
    handleScroll() {
      const sections = ["home", "about", "product", "contact"];

      if (window.scrollY === 0) {
        this.activeSection = "home";
        return;
      }

      sections.forEach((section) => {
        const element = document.getElementById(section);
        if (element) {
          const rect = element.getBoundingClientRect();
          if (rect.top >= 0 && rect.top < window.innerHeight) {
            this.activeSection = section;
          }
        }
      });
      // Close mobile menu on scroll
      if (document.body.classList.contains("mobile-nav-active")) {
        this.toggleMobileMenu();
      }
    },
    isActive(section) {
      return this.activeSection === section;
    },
    setActive(section) {
      this.activeSection = section;
    },
    setActiveSectionOnRoute() {
      // Set 'product' as activeSection if route path matches a product detail page
      if (this.$route.path.includes("/product/")) {
        this.activeSection = "product";
      }
    },
    toggleMobileMenu() {
      document.body.classList.toggle("mobile-nav-active");

      const mobileNavToggleBtn = document.querySelector(".mobile-nav-toggle");
      mobileNavToggleBtn.classList.toggle("bi-list");
      mobileNavToggleBtn.classList.toggle("bi-x");
    },
    setLanguage(lang) {
      localStorage.setItem('app_lang', lang);
      sessionStorage.setItem('lang_popup_seen', 'true');
      window.location.reload(); 
    }
  },
};
</script>


<style scoped>
.header {
  padding: 10px 0 !important;
  min-height: 60px !important;
}
.header .logo img {
  max-height: 40px !important;
}
.header .sitename {
  font-size: 1.5rem !important;
}
</style>
