<template>
  <section id="organization" class="clients section light-background" style="border-top: 2px solid rgba(0, 0, 0, 0.1); border-bottom: 5px solid rgba(0, 0, 0, 0.1);">
    <div class="section-title" data-aos="fade-up" style="padding-bottom: 0px">
      <h2 style="color: black;">{{ t.partnership }}</h2>
    </div>
    <div class="container" data-aos="fade-up" style="margin-top: 50px;">
      <!-- Untuk layar besar -->
      <div class="row gy-4 justify-content-center d-none d-md-flex">
        <div
          v-for="(client, index) in clients"
          :key="index"
          class="col-xl-2 col-md-3 col-6 client-logo" style="padding: 0;"
        >
          <img :src="client.imgSrc" class="img-fluid" :alt="client.altText" />
        </div>
      </div>

      <!-- Slider untuk layar kecil -->
      <v-carousel
        class="d-md-none horizontal-slider"
        hide-delimiters
        show-arrows
        cycle
      >
        <v-carousel-item>
          <div class="slider-container">
            <div
              v-for="(client, index) in clients"
              :key="index"
              class="client-logo"
            >
              <img :src="client.imgSrc" class="img-fluid" :alt="client.altText" />
            </div>
          </div>
        </v-carousel-item>
      </v-carousel>
    </div>
</section>

</template>

<script>
export default {
  name: "PartnerSection",
  data() {
    return {
      clients: [
        { imgSrc: "assets/img/partner/meratus.png", altText: "Meratus Group" },
        { imgSrc: "assets/img/partner/fsa.png", altText: "Client 2" },
        { imgSrc: "assets/img/partner/sucofindo.png", altText: "Client 3" },
      ],
      currentLang: "en"
    };
  },
  computed: {
    t() {
      const isId = this.currentLang === "id";
      const isCn = this.currentLang === "cn";
      return {
        partnership: isId ? "Kami Menjalin Kemitraan Dengan Perusahaan Ini" : isCn ? "我们与这些公司建立了合作伙伴关系" : "We Are Engaged In a Partnership With This Company",
      };
    }
  },
  created() {
    this.currentLang = localStorage.getItem("app_lang") || "en";
  }
};
</script>

<style scoped>
.client-logo img {
  max-width: 100%;
  height: auto;
}

.row {
  display: flex;
  justify-content: center;
}

.client-logo {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0px;
  gap: 5px;
}

.horizontal-slider .slider-container {
  display: flex; 
  justify-content: center;
  align-items: center;
  width: 100%;
  gap: 20px;
}

.horizontal-slider .v-carousel__container {
  overflow-x: auto;
  display: flex;
  justify-content: center;
  align-items: center;
}

.horizontal-slider .v-carousel-item {
  width: 100%; /* Menyesuaikan slider dengan kontainer */
  display: flex;
  justify-content: center;
}

@media (max-width: 640px) {
  .client-logo img {
    padding: 0px;
  }
}
</style>
