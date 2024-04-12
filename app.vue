<template>  
  <div>
    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<style>
body{
  background-image: url('/images/background.svg');
  background-repeat: no-repeat;
  background-size: cover;
}
.page-enter-active,
.page-leave-active {
  transition: all 0.4s;
}
.page-enter-from,
.page-leave-to {
  opacity: 0.5;
  /* filter: blur(1rem); */
  filter: grayscale(1)
}
</style>
