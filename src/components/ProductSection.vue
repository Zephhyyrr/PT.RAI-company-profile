<template>
  <section id="product" class="features section">
    <div class="container section-title" data-aos="fade-up">
      <h2 style="color: white">Product</h2>
      <p style="color: white">
        Our products are sourced directly from spice farmers in Indonesia
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
                product.images.length > 0
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
            Cinnamon Form
          </h2>

          <!-- Limit to the first 3 items -->
          <div
            v-for="(item, index) in cinnamonDetails.slice(0, 3)"
            :key="index"
          >
            <h5>{{ item.title }}</h5>
            <p style="text-align: justify">
              <strong v-if="item['sub-title']">Sub-title:</strong>
              {{ item["sub-title"] }}<br />
              <strong>Description:</strong> {{ item.description }}<br />
              <strong>Usage:</strong> {{ item.usage }}
            </p>
          </div>
          <!-- Long Description (only once) -->
          <div v-if="longDescription" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              Premium Cinnamon from Kerinci
            </h4>
            <p style="text-align: justify">{{ longDescription }}</p>
          </div>

          <!-- Moisture and Humidity Content (only once) -->
          <div v-if="moistureHumidity" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              {{ moistureHumidity.title }}
            </h4>
            <p style="text-align: justify">
              <strong>Moisture Content:</strong>
              {{ moistureHumidity["Moisture Content"] }}<br />
              <strong>Humidity:</strong> {{ moistureHumidity.Humidity }}
            </p>
          </div>
        </div>
      </div>

      <div v-if="cocofiberDetails.length > 0" data-aos="fade-up">
        <div class="card mb-4" style="padding: 30px">
          <h2 class="section-header" style="text-align: center">
            Cocofiber Form
          </h2>

          <!-- Limit to the first 3 items -->
          <div
            v-for="(item, index) in cocofiberDetails.slice(0, 3)"
            :key="index"
          >
            <h5>{{ item.title }}</h5>
            <p style="text-align: justify">
              <strong v-if="item['sub-title']">Sub-title:</strong>
              {{ item["sub-title"] }}<br />
              <strong>Description:</strong> {{ item.description }}<br />
              <strong>Usage:</strong> {{ item.usage }}
            </p>
          </div>
          <!-- Long Description (only once) -->
          <div v-if="cocofiberLongDescription" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              Premium Cocofiber from Indonesia
            </h4>
            <p style="text-align: justify">{{ cocofiberLongDescription }}</p>
          </div>

          <!-- Moisture and Humidity Content (only once) -->
          <div v-if="cocofiberMoistureHumidity" style="margin-top: 20px">
            <h4 style="text-align: center; font-weight: bold">
              {{ cocofiberMoistureHumidity.title }}
            </h4>
            <p style="text-align: justify">
              <strong>Moisture Content:</strong>
              {{ cocofiberMoistureHumidity["Moisture Content"] }}<br />
              <strong>Impurities:</strong> {{ cocofiberMoistureHumidity.Humidity }}
            </p>
          </div>
        </div>
      </div>

      <div class="container section-title pt-5" data-aos="fade-up">
      <h2 style="color: white">We also provide other premium spice products from Indonesia.</h2>
      <p style="color: white">
        Let's Check the Detail Below
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
                product.images.length > 0
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
import products from "../data/products-en.json";
import cinnamonDetails from "../data/cinnamon-general.json";
import cocofiberDetails from "../data/cocofiber-general.json";

export default {
  name: "ProductSection",
  data() {
    return {
      products,
      cinnamonDetails,
      cocofiberDetails,
      longDescription: null,
      moistureHumidity: null,
      cocofiberLongDescription: null,
      cocofiberMoistureHumidity: null,
    };
  },
  created() {
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
