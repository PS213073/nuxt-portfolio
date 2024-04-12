<template>
  <slot :posts="posts">
    <section class="not-prose mono-font">
      <div class="column text-gray-400 text-sm">
        <div>date</div>
        <div>title</div>
      </div>

      <ul>
        <li v-for="post in posts" :key="post._path">
          <NuxtLink
            :to="post._path"
            class="column hover:bg-gray-100 dark:hover:bg-gray-800"
          >
            <div
              :class="{
                'text-transparent dark:text-transparent': !post.displayYear,
                'text-gray-400 dark:text-gray-500': post.displayYear,
              }"
            >
              {{ post.year }}
            </div>
            <div>{{ post.title }}</div>
          </NuxtLink>
        </li>
      </ul>
    </section>
  </slot>
</template>
  
  <script setup>
const props = defineProps({
  limit: {
    type: Number,
    default: null,
  },
});

const { data } = await useAsyncData("blog-list", () => {
  const query = queryContent("/blog")
    .where({ _path: { $ne: "/blog" } })
    .only(["title", "_path", "publishedAt"])
    .sort({ publishedAt: -1 })

  if(props.limit){
    query.limit(props.limit)
  }
    return query.find();
});

const posts = computed(() => {
  if (!data.value) {
    return [];
  }
  const result = [];
  let lastYear = null;

  for (const post of data.value) {
    const year = new Date(post.publishedAt).getFullYear();
    // console.log(year);
    const displayYear = year !== lastYear;
    // console.log(`Should display a year ${displayYear}`);
    post.displayYear = displayYear;
    post.year = year;
    result.push(post);
    lastYear = year;
  }

  return result;
});

// Alternate
// const posts = computed(() => {
//   if (!data.value) {
//     return [];
//   }
//   const result = [];
//   const years = new Set();
//   for (const post of data.value) {
//     const year = new Date(post.publishedAt).getFullYear();
//     if (years.has(year)) {
//       post.displayYear = false;
//     } else {
//       years.add(year);
//       post.displayYear = true;
//     }
//     post.year = year;
//     result.push(post);
//   }
//   return result;
// });
</script>

<style scoped>
.column {
  @apply flex items-center space-x-8 py-2 border-b border-gray-200 dark:border-gray-700;
}
</style>