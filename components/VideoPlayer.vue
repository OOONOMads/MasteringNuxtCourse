<script setup>
const props = defineProps({
  videoId: {
    type: Number,
    required: true,
  },
});
</script>

<template>
  <iframe :src="`https://player.vimeo.com/video/${props.videoId}`" title="Video player" frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen></iframe>
</template>

<style scoped>
iframe {
  margin: 50px 0;
}
</style>
