<script setup lang="ts">
defineProps<{
    title: string;
    channel: string;
    views: string;
    thumbnail: string;
}>();

const emit = defineEmits(['liked'])

function like() {
  emit('liked')  // отправляем событие родителю
}
</script>

<template>
    <div class="video_card">
        <p> title: {{ title }}</p>
        <p> channel: {{ channel }}</p>
        <p> views: {{  views }}</p>
        <p> thumbnail: {{ thumbnail }}</p>
        <button @click="$emit('liked')"> ❤■ </button>
    </div>
</template>

