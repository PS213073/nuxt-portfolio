<template>
    <div>Projects</div>
    <section v-if="pending">Loading ...</section>
    <section v-else-if="error">Something went wrong... Try again!</section>
    <section v-else>Here we are display the repos!</section>
</template>

<script setup>
const { error, pending, data } = await useFetch(
  "https://api.github.com/users/PS213073/repos"
);
</script>