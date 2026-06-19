<template>
  <section id="contact" class="contact section light-background" style="padding: 0;">
    <!-- Section Title -->
    <div class="container section-title" data-aos="fade-up" style="padding-top: 30px;">
      <h2>{{ t.contact }}</h2>
      <p>{{ t.contactUsHere }}</p>
    </div>

    <div class="container" data-aos="fade-up" data-aos-delay="100">
  <div class="row gy-4">
    <div class="col-lg-3 col-md-6 col-sm-6">
      <a href="https://maps.app.goo.gl/3H5LWyxHy4ywKMm8A" target="_blank" style="text-decoration: none; color: inherit">
        <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="600" style="height: 100%; cursor: pointer">
          <img src="/assets/img/images/icons/ic_maps.png" alt="WhatsApp Icon" style="width: 55px; height: 55px" />
          <h3>{{ t.address }}</h3>
          <p style="text-align: center">Jl. Raya Nanggalo No. 28 A, Kp. Olo, Nanggalo District, Padang City, West Sumatera, 25173 - Indonesia</p>
        </div>
      </a>
    </div>

    <div class="col-lg-3 col-md-6 col-sm-6">
      <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="400" style="height: 100%">
        <img src="/assets/img/images/icons/ic_wa.png" alt="WhatsApp Icon" style="width: 75px; height: 75px" />
        <h3>{{ t.chatOnWhatsapp }}</h3>
        <p><a href="https://wa.me/6282374635328" target="_blank" style="color: #000;">+6282374635328 (Alno Ramalino)</a></p>
        <p><a href="https://wa.me/6281275341600" target="_blank" style="color: #000;">+6281275341600 (Anjas)</a></p>
      </div>
    </div>

    <div class="col-lg-3 col-md-6 col-sm-6">
      <a href="https://www.instagram.com/pt.rumpunalamindonesia/?utm_source=ig_web_button_share_sheet" target="_blank" style="text-decoration: none; color: inherit">
        <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="600" style="height: 100%; cursor: pointer">
          <img src="/assets/img/images/icons/ic_ig.png" alt="WhatsApp Icon" style="width: 75px; height: 75px" />
          <h3>{{ t.followOurInstagram }}</h3>
          <p>pt.rumpunalamindonesia</p>
        </div>
      </a>
    </div>

    <div class="col-lg-3 col-md-6 col-sm-6">
      <a href="https://www.linkedin.com/in/rumpun-alam-indonesia-584a84336/" target="_blank" style="text-decoration: none; color: inherit">
        <div class="info-item d-flex flex-column justify-content-center align-items-center" data-aos="fade-up" data-aos-delay="600" style="height: 100%; cursor: pointer">
          <img src="/assets/img/images/icons/ic_linkedin.png" alt="WhatsApp Icon" style="width: 50px; height: 50px" />
          <h3>{{ t.connectWithOurLinkedin }}</h3>
          <p>Rumpun Alam Indonesia</p>
        </div>
      </a>
    </div>
  </div>

  <div class="row gy-4 mt-1">
    <div class="col-lg-6" data-aos="fade-up" data-aos-delay="300">
      <iframe src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d249.33308816538693!2d100.36415625984897!3d-0.8969739504729131!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sid!2sid!4v1730645933044!5m2!1sid!2sid" frameborder="0" style="border: 0; width: 100%; height: 400px" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
    </div>

    <div class="col-lg-6">
      <form @submit.prevent="sendEmail" class="php-email-form" data-aos="fade-up" data-aos-delay="400">
        <div class="row gy-4">
          <div class="col-md-12">
            <input type="text" v-model="name" class="form-control" :placeholder="t.yourName" required />
          </div>
          <div class="col-md-12">
            <input type="text" v-model="subject" class="form-control" :placeholder="t.subject" required />
          </div>
          <div class="col-md-12">
            <textarea v-model="message" class="form-control" rows="6" :placeholder="t.message" required></textarea>
          </div>

          <!-- hCaptcha Widget -->
          <div class="col-md-12">
            <div class="h-captcha" :data-sitekey="hcaptchaSiteKey"></div>
          </div>

          <!-- Honeypot for bot detection -->
          <div style="display: none">
            <input type="text" v-model="honeypot" name="honeypot" />
          </div>

          <div class="col-md-12 text-center">
            <button type="submit" style="background-color: #007a08; color: white;">{{ t.sendMessage }}</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</div>

  </section>
</template>

<script>
export default {
  name: "ContactSection",
  data() {
    return {
      name: "",
      subject: "",
      message: "",
      honeypot: "",
      lastSubmit: null,
      hcaptchaSiteKey: "81be2c46-9600-47d2-b334-d8268a36d8c8",
      hcaptchaLoaded: false,
      currentLang: "en"
    };
  },
  computed: {
    t() {
      const isId = this.currentLang === "id";
      const isCn = this.currentLang === "cn";
      return {
        contact: isId ? "Kontak" : isCn ? "联系我们" : "Contact",
        contactUsHere: isId ? "Hubungi kami di sini" : isCn ? "在这里联系我们" : "Contact us here",
        address: isId ? "Alamat" : isCn ? "地址" : "Address",
        chatOnWhatsapp: isId ? "Chat di WhatsApp" : isCn ? "在WhatsApp上聊天" : "Chat on WhatsApp",
        followOurInstagram: isId ? "Ikuti Instagram Kami" : isCn ? "关注我们的Instagram" : "Follow Our Instagram",
        connectWithOurLinkedin: isId ? "Terhubung di LinkedIn Kami" : isCn ? "连接我们的LinkedIn" : "Connect With Our LinkedIn",
        yourName: isId ? "Nama Anda" : isCn ? "您的名字" : "Your Name",
        subject: isId ? "Subjek" : isCn ? "主题" : "Subject",
        message: isId ? "Pesan" : isCn ? "信息" : "Message",
        sendMessage: isId ? "Kirim Pesan" : isCn ? "发送信息" : "Send Message"
      };
    }
  },
  created() {
    this.currentLang = localStorage.getItem("app_lang") || "en";
  },
  mounted() {
    this.loadHcaptcha();
  },
  methods: {
    loadHcaptcha() {
      const script = document.createElement("script");
      script.src = "https://hcaptcha.com/1/api.js";
      script.async = true;
      script.defer = true;
      script.onload = () => {
        this.hcaptchaLoaded = true;
        console.log("hCaptcha script loaded.");
      };
      script.onerror = () => {
        console.error("Failed to load hCaptcha script.");
      };
      document.head.appendChild(script);
    },
    sendEmail() {
      if (!this.hcaptchaLoaded) {
        console.error("hCaptcha script not loaded.");
        alert("hCaptcha script not loaded. Please try again.");
        return;
      }

      const hcaptchaResponse = window.hcaptcha.getResponse();
      if (!hcaptchaResponse) {
        alert("Please complete the CAPTCHA.");
        return;
      }

      if (this.honeypot) {
        console.log("Bot detected!");
        return;
      }

      const now = new Date().getTime();
      if (this.lastSubmit && now - this.lastSubmit < 30000) {
        alert("You are submitting too quickly. Please wait a moment.");
        return;
      }

      this.lastSubmit = now;

      const spamKeywords = ["free", "offer", "buy now"];
      if (
        this.subject &&
        spamKeywords.some((keyword) =>
          this.subject.toLowerCase().includes(keyword)
        )
      ) {
        alert("The subject contains spammy content. Please modify it.");
        return;
      }

      const emailSubject = encodeURIComponent(this.subject);
      const emailBody = encodeURIComponent(
        `Name: ${this.name}\n\nMessage: ${this.message}`
      );

      const mailtoLink = `https://mail.google.com/mail/?view=cm&fs=1&to=rumpunalamindonesia@gmail.com&su=${emailSubject}&body=${emailBody}`;

      window.location.href = mailtoLink;
    },
  },
};
</script>
