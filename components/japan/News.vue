<template>
  <div
    class="mx-auto px-4 sm:px-6 relative z-10 lg:flex items-center justify-center"
  >
    <div class="sm:mr-12 mb-6" data-aos="zoom-out-right">
      <img
        class="mx-auto max-w-[280px] sm:max-w-[400px] lg:max-w-none"
        src="/images/japan/news-image.svg"
        alt="News"
        width="670"
        height="564"
      />
    </div>
    <div class="max-w-3xl">
      <h2 class="title mb-6 sm:mb-10 text-center lg:text-left">
        <span>News</span>
      </h2>
      <ul class="space-y-6">
        <li v-for="post in posts" class="sm:flex">
          <time class="w-36 shrink-0 block text-gray-400 text-sm sm:text-base">
            {{ post.publishedDate }}
          </time>
          <NuxtLink
            :to="post.href"
            class="hover:underline transition hover:text-space-cyan-light"
          >
            {{ post.title }}
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup lang="ts">
import gql from "graphql-tag";

// The subsocial space for news: https://polkaverse.com/10802 , and Japanese: https://polkaverse.com/11315
const { locale } = useI18n();
const astarSpace = locale.value === "ja" ? 11315 : 10802;
const query = gql`
  query PostsBySpaceId {
    posts(where: { space: { id_eq: "${astarSpace}" }, tagsOriginal_containsInsensitive: "japan", hidden_eq: false }, orderBy: id_DESC) {
      publishedDate: createdOnDay
      title
      href: canonical
      slug
      id
    }
  }
`;

const { data } = await useAsyncQuery({ query, clientId: "subsocial" });
const posts = data.value.posts.map(
  (item: { publishedDate: string | number | Date }) => {
    const date = new Date(item.publishedDate);
    const formattedDate = date.toLocaleDateString("en-US", {
      month: "short",
      day: "numeric",
      year: "numeric",
    });
    return {
      ...item,
      publishedDate: formattedDate,
    };
  }
);
</script>
