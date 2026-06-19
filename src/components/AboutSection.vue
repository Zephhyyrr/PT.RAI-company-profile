<template>
  <!-- About Section -->
  <section id="about" class="about section light-background">
    <div class="container">
      <div class="row gy-4">
        <div class="col-lg-6 content" data-aos="fade-up" data-aos-delay="100">
          <div v-if="currentLang === 'en'">
            <p class="who-we-are">Who We Are</p>
            <h3>Rumpun Alam Indonesia</h3>
            <p class="text-justify" style="text-align: justify;">
              PT. Rumpun Alam Indonesia is one of the businesses that started in
              2021 starting in the field of manufacturing, processing (production)
              of local spices that dominate the natural harvest of West Sumatra
              Indonesia which is monitored and supervised directly by the West
              Sumatra provincial trade and agriculture office for feasibility
              testing and food security. The processing existence began to develop
              in 2022. Where this place is a unit from the planting process to the
              processing of the entire harvest which is manual so that it requires
              a relatively large workforce even though not all workers do sorting
              at the production site. with a lot of market demand and a lot of
              interest and demand for export and import from various countries
              regarding this in 2023 we officially investigate PT or a company
              that is registered and incorporated with the official legality of
              Indonesian nationality.
            </p>
            <ul>
              <p class="fst fs-6 fw-bold">
                PT Rumpun Alam Indonesia mission and objectives :
              </p>
              <li>
                <span style="text-align: justify;"
                  >Introducing the natural wealth of West Sumatra - Indonesia to
                  the wider community both locally and internationally</span
                >
              </li>
              <li>
                <span style="text-align: justify;"
                  >Preserving Indonesia's heritage and culture as an
                  internationally recognized spice producer
                </span>
              </li>
              <li>
                <span style="text-align: justify;">Helps add to the country's foreign exchange</span>
              </li>
              <li>
                <span style="text-align: justify;"
                  >Striving to uplift the dignity and well-being of the
                  surrounding environment</span
                >
              </li>
            </ul>
            <p class="fst fs-6 fw-bold">
              While the purpose of pt rumpun alam indonesia itself is to maximize
              profits (profitability) as companies in general.
            </p>
            <p class="fst fs-6 fw-bold">Yield and marketing :</p>
            <p style="text-align: justify;">
              PT Rumpun Alam Indonesia produces a variety of traditional spices of
              natural cultural heritage. In addition, West Sumatra is a
              combination of geographical structures that greatly affect the
              natural wealth that produces an image of biodiversity which has the
              function of providing the needs of other living things, such as
              clothing, food and medicine.
            </p>
          </div>
          <div v-else-if="currentLang === 'cn'">
            <p class="who-we-are">关于我们</p>
            <h3>Rumpun Alam Indonesia</h3>
            <p class="text-justify" style="text-align: justify;">
              PT. Rumpun Alam Indonesia 成立于2021年，是一家从事制造和加工（生产）当地香料的企业。这些香料在印度尼西亚西苏门答腊省的自然收成中占主导地位。该过程由西苏门答腊省贸易和农业部门直接监控和监督，以进行可行性测试和食品安全保障。加工业务在2022年开始发展。在这里，从种植到全部收成的加工过程是一体化的。大部分操作通过手工完成，因此需要大量劳动力，尽管并非所有工人都在生产现场进行分拣。随着市场需求的大幅增加以及各国进出口意愿的提高，2023年我们正式成立了PT（有限责任公司），这是一家在印度尼西亚具有官方合法地位的注册法人企业。
            </p>
            <ul>
              <p class="fst fs-6 fw-bold">
                PT Rumpun Alam Indonesia 的使命和目标：
              </p>
              <li>
                <span style="text-align: justify;"
                  >向国内外更广泛的社会介绍印度尼西亚西苏门答腊省的自然财富。</span
                >
              </li>
              <li>
                <span style="text-align: justify;"
                  >维护印度尼西亚作为国际公认的香料生产国的文化与遗产。
                </span>
              </li>
              <li>
                <span style="text-align: justify;">协助增加国家外汇收入。</span>
              </li>
              <li>
                <span style="text-align: justify;"
                  >致力于提升周边环境和社区的尊严与福祉。</span
                >
              </li>
            </ul>
            <p class="fst fs-6 fw-bold">
              与此同时，PT Rumpun Alam Indonesia 的主要目标与一般企业一样，是实现利润（盈利能力）最大化。
            </p>
            <p class="fst fs-6 fw-bold">产品与营销：</p>
            <p style="text-align: justify;">
              PT Rumpun Alam Indonesia 生产各种传统香料，这些香料是自然文化的遗产。此外，西苏门答腊省独特的地理结构极大影响了其自然资源，产生了丰富的生物多样性。这些资源能够满足人类及其他生物的需求，如服装、食品和药品。
            </p>
          </div>
          <div v-else>
            <p class="who-we-are">Siapa Kami</p>
            <h3>Rumpun Alam Indonesia</h3>
            <p class="text-justify" style="text-align: justify;">
              PT. Rumpun Alam Indonesia adalah salah satu usaha yang berdiri pada tahun 2021 dan bergerak di bidang manufaktur, pengolahan (produksi) rempah-rempah lokal yang mendominasi hasil alam Sumatera Barat, Indonesia. Proses ini dipantau dan diawasi langsung oleh dinas perdagangan dan pertanian provinsi Sumatera Barat untuk uji kelayakan dan ketahanan pangan. Eksistensi pengolahan mulai berkembang pada tahun 2022. Di mana tempat ini merupakan satu kesatuan mulai dari proses penanaman hingga pengolahan seluruh hasil panen yang dilakukan secara manual sehingga membutuhkan tenaga kerja yang relatif banyak meskipun tidak semua pekerja melakukan penyortiran di lokasi produksi. Dengan banyaknya permintaan pasar serta tingginya minat ekspor dan impor dari berbagai negara, pada tahun 2023 kami resmi mendirikan PT atau perusahaan yang terdaftar dan berbadan hukum dengan legalitas resmi kebangsaan Indonesia.
            </p>
            <ul>
              <p class="fst fs-6 fw-bold">
                Misi dan tujuan PT Rumpun Alam Indonesia :
              </p>
              <li>
                <span style="text-align: justify;"
                  >Memperkenalkan kekayaan alam Sumatera Barat - Indonesia kepada masyarakat luas baik secara lokal maupun internasional</span
                >
              </li>
              <li>
                <span style="text-align: justify;"
                  >Melestarikan warisan dan budaya Indonesia sebagai produsen rempah-rempah yang diakui secara internasional
                </span>
              </li>
              <li>
                <span style="text-align: justify;">Membantu menambah devisa negara</span>
              </li>
              <li>
                <span style="text-align: justify;"
                  >Berusaha mengangkat harkat dan martabat serta kesejahteraan lingkungan sekitar</span
                >
              </li>
            </ul>
            <p class="fst fs-6 fw-bold">
              Sementara tujuan utama dari PT Rumpun Alam Indonesia sendiri adalah untuk memaksimalkan keuntungan (profitabilitas) seperti perusahaan pada umumnya.
            </p>
            <p class="fst fs-6 fw-bold">Hasil dan Pemasaran :</p>
            <p style="text-align: justify;">
              PT Rumpun Alam Indonesia memproduksi berbagai rempah-rempah tradisional yang merupakan warisan budaya alam. Selain itu, Sumatera Barat memiliki kombinasi struktur geografis yang sangat mempengaruhi kekayaan alamnya, menghasilkan keanekaragaman hayati yang berfungsi untuk memenuhi kebutuhan makhluk hidup lainnya, seperti sandang, pangan, dan obat-obatan.
            </p>
          </div>
        </div>

        <div
          class="col-lg-6 about-images"
          data-aos="fade-up"
          data-aos-delay="200"
        >
          <div class="row gy-4">
            <div class="col-3 col-sm-6 p-3">
              <img
                src="/assets/img/images/kayumanis-version/CinnamonStick-6cm.png"
                class="img-fluid"
                alt=""
              />
            </div>
            <div class="col-3 col-sm-6 p-3">
              <img
                src="/assets/img/images/cocofiber/cocofiber1.jpeg"
                class="img-fluid"
                alt=""
              />
            </div>
            <div class="col-3 col-sm-6 p-3">
              <img
                src="/assets/img/images/kayumanis-version/Cinnamon-KF.png"
                class="img-fluid"
                alt=""
              />
            </div>
            <div class="col-3 col-sm-6 p-3">
              <img
                src="/assets/img/images/kayumanis-version/Cinnamon-KA/KB.png"
                class="img-fluid"
                alt=""
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!-- /About Section -->
</template>

<script>
export default {
  name: "AboutSection",
  data() {
    return {
      currentLang: "en"
    };
  },
  created() {
    this.currentLang = localStorage.getItem("app_lang") || "en";
  }
};
</script>

<style scoped>
.about-images .col-3 {
  padding: 0; /* Remove padding between images */
}

.about-images img {
  width: 100%;
  aspect-ratio: 4 / 3;
  object-fit: cover;
  border-radius: 12px;
}

@media (max-width: 576px) {
  .about-images .col-3 {
    flex: 0 0 50%; /* 4 images per row on mobile devices */
    max-width: 50%; /* Ensure that each image takes up 25% of the row */
  }
}
</style>
