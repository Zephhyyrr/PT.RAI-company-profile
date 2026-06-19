<template>
  <section id="product" class="features section">
    <div class="container section-title" data-aos="fade-up">
      <h2 style="color: white">{{ t.product }}</h2>
      <p style="color: white">
        {{ t.ourProducts }}
      </p>
    </div>

    <div class="container">
      <div class="row d-flex justify-content-center" data-aos="fade-up">
        <div
          class="col-lg-3 col-md-4 col-sm-6 mb-4"
          v-for="product in products.slice(0, 4)"
          :key="product.id"
        >
          <router-link
            :to="`/product/${product.id}`"
            class="card h-100 shadow-card"
          >
            <img
              class="card-img-top"
              :src="
                product.images && product.images.length > 0
                  ? product.images[0]
                  : 'https://via.placeholder.com/300x200'
              "
              :alt="product.title"
            />
            <div class="card-body text-center">
              <h5 class="card-title text-success fw-bold">
                {{ product.title }}
              </h5>
              <p class="card-text text-muted">{{ product.short }}</p>
              <p class="card-text text-muted">{{ product.details }}</p>
            </div>
          </router-link>
        </div>
      </div>

      <div v-if="cinnamonDetails.length > 0" data-aos="fade-up">
        <div class="card mb-4" style="padding: 30px">
          <h2 class="section-header" style="text-align: center">
            {{ t.cinnamonForm }}
          </h2>

          <!-- Limit to the first 3 items -->
          <div
            v-for="(item, index) in cinnamonDetails.slice(0, 3)"
            :key="index"
          >
            <h5>{{ item.title }}</h5>
            <p style="text-align: justify">
              <strong v-if="item['sub-title']">{{ t.subtitle }}</strong>
              {{ item["sub-title"] }}<br />
              <strong>{{ t.description }}</strong> {{ item.description }}<br />
              <strong>{{ t.usage }}</strong> {{ item.usage }}
            </p>
          </div>
          <!-- Long Description (only once) -->
          <div v-if="longDescription" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              {{ t.premiumCinnamon }}
            </h4>
            <p style="text-align: justify">{{ longDescription }}</p>
          </div>

          <!-- Moisture and Humidity Content (only once) -->
          <div v-if="moistureHumidity" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              {{ moistureHumidity.title }}
            </h4>
            <p style="text-align: justify">
              <strong>{{ t.moistureContent }}</strong>
              {{ moistureHumidity["Moisture Content"] }}<br />
              <strong>{{ t.humidity }}</strong> {{ moistureHumidity.Humidity }}
            </p>
          </div>
        </div>
      </div>

      <div v-if="cocofiberLongDescription || cocofiberMoistureHumidity" data-aos="fade-up">
        <div class="card mb-4" style="padding: 30px">
          <!-- Long Description (only once) -->
          <div v-if="cocofiberLongDescription">
            <h4 style="text-align: center; font-weight: bold">
              {{ t.premiumCocofiber }}
            </h4>
            <p style="text-align: justify">{{ cocofiberLongDescription }}</p>
          </div>

        </div>
      </div>

      <div class="container section-title pt-5" data-aos="fade-up">
      <h2 style="color: white">{{ t.otherProducts }}</h2>
      <p style="color: white">
        {{ t.checkDetail }}
      </p>
    </div>
      <div class="row d-flex justify-content-center" data-aos="fade-up">
        <div
          class="col-lg-3 col-md-4 col-sm-6 mb-4"
          v-for="product in products.slice(4)"
          :key="product.id"
        >
          <router-link
            :to="`/product/${product.id}`"
            class="card h-100 shadow-card"
          >
            <img
              class="card-img-top"
              :src="
                product.images && product.images.length > 0
                  ? product.images[0]
                  : 'https://via.placeholder.com/300x200'
              "
              :alt="product.title"
            />
            <div class="card-body text-center">
              <h5 class="card-title text-success fw-bold">
                {{ product.title }}
              </h5>
              <p class="card-text text-muted">{{ product.short }}</p>
              <p class="card-text text-muted">{{ product.details }}</p>
            </div>
          </router-link>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
// Import the JSON data
import productsEn from "../data/products-en.json";
import productsId from "../data/products-id.json";
import cinnamonDetailsEn from "../data/cinnamon-general.json";
import cocofiberDetailsEn from "../data/cocofiber-general.json";
import cinnamonDetailsId from "../data/cinnamon-general-id.json";
import cocofiberDetailsId from "../data/cocofiber-general-id.json";

export default {
  name: "ProductSection",
  data() {
    return {
      products: [],
      cinnamonDetails: [],
      cocofiberDetails: [],
      longDescription: null,
      moistureHumidity: null,
      cocofiberLongDescription: null,
      cocofiberMoistureHumidity: null,
      currentLang: "en"
    };
  },
  computed: {
    t() {
      const isId = this.currentLang === "id";
      return {
        product: isId ? "Produk" : "Product",
        ourProducts: isId ? "Produk kami didapatkan langsung dari petani rempah di Indonesia" : "Our products are sourced directly from spice farmers in Indonesia",
        cinnamonForm: isId ? "Bentuk Kayu Manis" : "Cinnamon Form",
        subtitle: isId ? "Sub-judul:" : "Sub-title:",
        description: isId ? "Deskripsi:" : "Description:",
        usage: isId ? "Penggunaan:" : "Usage:",
        premiumCinnamon: isId ? "Kayu Manis Premium dari Kerinci" : "Premium Cinnamon from Kerinci",
        moistureContent: isId ? "Kadar Air:" : "Moisture Content:",
        humidity: isId ? "Kelembapan:" : "Humidity:",
        premiumCocofiber: isId ? "Cocofiber Premium dari Indonesia" : "Premium Cocofiber from Indonesia",
        impurities: isId ? "Kotoran:" : "Impurities:",
        otherProducts: isId ? "Kami juga menyediakan produk rempah premium lainnya dari Indonesia." : "We also provide other premium spice products from Indonesia.",
        checkDetail: isId ? "Lihat Detail di Bawah" : "Let's Check the Detail Below",
      };
    }
  },
  created() {
    this.currentLang = localStorage.getItem("app_lang") || "en";
    
    if (this.currentLang === "id") {
      this.products = productsId.filter(p => p.id !== "cardamom");
      this.cinnamonDetails = cinnamonDetailsId;
      this.cocofiberDetails = cocofiberDetailsId;
    } else {
      this.products = productsEn.filter(p => p.id !== "cardamom");
      this.cinnamonDetails = cinnamonDetailsEn;
      this.cocofiberDetails = cocofiberDetailsEn;
    }

    const longDescriptionItem = this.cinnamonDetails.find(
      (item) => item["long-description"]
    );
    if (longDescriptionItem) {
      this.longDescription = longDescriptionItem["long-description"];
    }

    const moistureHumidityItem = this.cinnamonDetails.find(
      (item) => item["Moisture Content"]
    );
    if (moistureHumidityItem) {
      this.moistureHumidity = {
        title: moistureHumidityItem.title,
        "Moisture Content": moistureHumidityItem["Moisture Content"],
        Humidity: moistureHumidityItem.Humidity,
      };
    }

    const cocoLongDescriptionItem = this.cocofiberDetails.find(
      (item) => item["long-description"]
    );
    if (cocoLongDescriptionItem) {
      this.cocofiberLongDescription = cocoLongDescriptionItem["long-description"];
    }

    const cocoMoistureHumidityItem = this.cocofiberDetails.find(
      (item) => item["Moisture Content"]
    );
    if (cocoMoistureHumidityItem) {
      this.cocofiberMoistureHumidity = {
        title: cocoMoistureHumidityItem.title,
        "Moisture Content": cocoMoistureHumidityItem["Moisture Content"],
        Humidity: cocoMoistureHumidityItem.Humidity,
      };
    }
  },
};
</script>
<style scoped>
.card {
  border-radius: 10px;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  text-decoration: none;
  color: inherit;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.shadow-card {
  box-shadow: 0 8px 8px rgba(0, 0, 0, 0.1);
}

.card-img-top {
  height: 200px;
  object-fit: cover;
}

.card-body {
  padding: 15px;
}

.section-header {
  margin-top: 30px;
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  color: #333;
}

.mb-4 {
  margin-bottom: 20px;
}
</style>
