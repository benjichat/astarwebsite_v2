<template>
  <div class="max-w-7xl mx-auto px-4 sm:px-6 relative z-10">
    <h2 class="title text-center mb-12 sm:mb-16"><span>Astar Blog</span></h2>
    <ul class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8 lg:gap-12">
      <BlogArticleCard v-for="post in posts" :post="post" />
    </ul>
    <div class="text-center mt-12 sm:mt-20">
      <Button size="lg" :href="localePath('/blog')">Astar Blog -></Button>
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
    posts(where: { space: { id_eq: "${astarSpace}" } }, orderBy: id_DESC, limit: 6) {
      publishedDate: createdOnDay
      title
      href: canonical
      image
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
      image: item.image
        ? "https://ipfs.subsocial.network/ipfs/" + item.image
        : "/images/blog/placeholder.webp",
      publishedDate: formattedDate,
    };
  }
);

const localePath = useLocalePath();
</script>
