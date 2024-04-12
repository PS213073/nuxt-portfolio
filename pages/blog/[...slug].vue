<template>
  <article
    class="prose dark:prose-invert prose-h1:font-semibold prose-pre:bg-white dark:prose-pre:bg-gray-800 prose-pre:text-gray-700 dark:prose-pre:text-gray-300 max-w-none"
  >
    <ContentDoc v-slot="{ doc }">
      <div class="grid grid-cols-6 gap-20">
        <div
          :class="{
            'col-span-6 md:col-span-4': doc.toc,
            'col-span-6': !doc.toc,
          }"
        >
          <ContentRenderer :value="doc" />
        </div>
        <div class="hidden md:col-span-2 md:block not-prose" v-if="doc.toc">
          <aside class="sticky top-8">
            <div class="font-semibold mb-2">Table of Contents</div>
            <nav>
              <TocLinks :links="doc.body.toc.links" :active-id="activeId" />
            </nav>
          </aside>
        </div>
      </div>
    </ContentDoc>
  </article>
</template>

<script setup>
const activeId = ref(null)
onMounted(() => {
  const callback = (entries) => {
    for (const entry of entries){
      if(entry.isIntersecting){
        activeId.value = entry.target.id
        break;
      }
    }
  };

  const observer = new IntersectionObserver(callback, {
    root: null,
    threshold: 0.5,
  })
  const elements = document.querySelectorAll('h2', 'h3')

  for (const element of elements){
    observer.observe(element)
  }

  onBeforeUnmount(() => {
    // console.log('onBeforeUnmount');
    for (const elemet of elements){
      observer.unobserve(elemet)
    }
  })
})
</script>