<template>
  <NuxtLayout name="default">
    <template #space>
      <!-- <div class="banner--hiring">
        <NuxtLink
          to="https://wellfound.com/company/astar-network"
          target="_blank"
          class="link--hiring"
        >
          {{ $t("home.hiring") }}
          <ArrowTopRightOnSquareIcon class="w-5 h-5 ml-1 stroke-2" />
        </NuxtLink>
      </div> -->
      <div class="bg-black">
        <div class="absolute z-0 w-full h-screen flex items-center">
          <ScrollParallax :speed="0.25" class="mx-auto">
            <video
              webkit-playsinline
              playsinline
              muted
              autoplay
              loop
              data-not-lazy
            >
              <source src="/videos/astar.mp4" type="video/mp4" />
            </video>
          </ScrollParallax>
        </div>
        <div class="space-gradient before:hidden mix-blend-screen">
          <img
            class="absolute z-[1] mix-blend-overlay portrait:h-screen landscape:w-screen object-cover"
            src="/images/common/space-cloud.webp"
            alt=""
            width="1728"
            height="1281"
            data-not-lazy
          />
          <img
            class="fixed z-[2] portrait:h-screen landscape:w-screen object-cover"
            src="/images/common/space-stars.svg"
            alt=""
            width="1728"
            height="1728"
            data-not-lazy
          />
          <HomeHero />
          <div class="welcome-bg -mt-44 pt-44 pb-32 sm:pb-64">
            <HomeWelcome />
          </div>
        </div>
      </div>

      <HomeFeaturedContents />

      <HomeBecomeAStar class="pt-32 sm:pt-64 pb-32 sm:pb-64" />

      <HomeRecommendedReading class="sm:py-24" />

      <HomeNewsletter class="pb-12 sm:py-12" />
    </template>

    <template #earth>
      <div class="sky-gradient">
        <div class="sky-gradient-inner">
          <HomeFeatures class="pt-12 pb-32 sm:pb-56" />
          <HomeBackers />
          <img
            class="w-full"
            src="/images/home/footer-sky.svg"
            alt=""
            width="1728"
            height="290"
            data-not-lazy
          />
          <img
            class="w-full"
            src="/images/home/footer-landscape.svg"
            alt=""
            width="1728"
            height="220"
            data-not-lazy
          />
        </div>
      </div>
      <div class="footer">
        <div class="footer-inner pt-12 sm:pt-28">
          <Footer color="light" />
        </div>
      </div>
    </template>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { ArrowTopRightOnSquareIcon } from "@heroicons/vue/24/outline";
import ScrollParallax from "vue3-parallax/src/components/ScrollParallax.vue";

import { meta } from "@/content/meta";
const { t } = useI18n();
const seoTitle = `${meta.siteName} - ${t("meta.tagline")}`;
const seoDescription = t("meta.description");
const seoUrl = meta.url;
const seoImage = `${meta.image}common.png`;

useServerSeoMeta({
  title: () => seoTitle,
  description: () => seoDescription,
  ogTitle: () => seoTitle,
  ogDescription: () => seoDescription,
  ogImage: () => seoImage,
  ogImageUrl: () => seoImage,
  ogType: () => "website",
  ogUrl: () => seoUrl,
  twitterCard: () => "summary_large_image",
  twitterTitle: () => seoTitle,
  twitterDescription: () => seoDescription,
  twitterImage: () => seoImage,
});

definePageMeta({
  layout: false,
});
</script>

<style lang="postcss" scoped>
.banner--hiring {
  background: rgba(255, 255, 255, 0.85);
  position: absolute;
  top: 0px;
  right: 0px;
  width: 220px;
  height: 30px;
  color: #fff;
  z-index: 9999;
  text-align: right;
  border-bottom-left-radius: 10px;
}
.link--hiring {
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(
    90deg,
    #e6007a -5.88%,
    #703ac2 15.42%,
    #0070eb 40.77%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  text-decoration: underline;
  font-weight: bold;
  color: #0070eb;
}
.welcome-bg {
  background: linear-gradient(
    0deg,
    rgba(8, 16, 41, 1) 50%,
    rgba(8, 16, 41, 0) 100%
  );
}
.sky-gradient {
  background: linear-gradient(
    90deg,
    #ffeff8 2.37%,
    #f0e7ff 22.25%,
    #dcedff 43.43%,
    #def2ff 68%,
    #d7faff 85.32%
  );
}
.sky-gradient-inner {
  background: linear-gradient(
    0deg,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 1) 100%
  );
}
.footer {
  background: linear-gradient(260deg, #3d41f8 0.16%, #58cef4 94.67%);
}
.footer-inner {
  background-image: url(/images/home/footer-reflect.svg);
  background-position: top center;
  background-size: 100%;
  background-repeat: no-repeat;
}
</style>
