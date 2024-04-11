<template>
   <article class="prose dark:prose-invert prose-h1:font-semibold">
    <ContentDoc/>
   </article>
</template>

<script setup>
const route = useRoute()
console.log(route.params.slug);
</script>