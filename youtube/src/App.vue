<script setup lang="ts">
import { ref, computed, watch} from "vue"
import VideoCard from "./components/VideoCard.vue"



// список видео
const list_of_videos = ref([
  { title: "title", channel: "channel", thumbnail: "thumbnail", views: "views" },
  { title: "new_title", channel: "new_channel", thumbnail: "new_thumbnail", views: "new_views" }
])

// строка фильтра (ввод пользователя)
const model = ref("")
const counter = ref(0)

//для лайков
const likes = ref(0)

// вычисляемый список отфильтрованных видео
const filtered_videos = computed(() => {
  if (!model.value) return list_of_videos.value
  return list_of_videos.value.filter(v =>
    v.title.toLowerCase().includes(model.value.toLowerCase()) ||
    v.channel.toLowerCase().includes(model.value.toLowerCase())
  ) 
})

// следим за изменением фильтра и увеличиваем просмотры
watch(filtered_videos, (newList) => {
  counter.value = newList.length
})

//функция обработки лайков
function likedVideos() {
  likes.value++;
}
</script>

<template>
  <div class="background">
  <h1 class="h1">List of videos</h1>

  <div class="input">

  <input class="button" v-model="model" placeholder="Поиск по названию или каналу" />
  
  <!-- отображаем количество найденных видео -->
  <p class="counter">Найдено: {{ counter }}</p>
  <p class="counter"> Общее количество лайков: {{ likes }}</p>
  </div>

  <ul>
    <div class="counter">
    <template v-if="filtered_videos.length > 0">
      <video-card
      v-for="(video, index) in filtered_videos"
      v-bind:key="index"
      v-bind:title="video.title"
      v-bind:channel="video.channel"
      v-bind:views="video.views"
      v-bind:thumbnail="video.thumbnail"
      @liked="likedVideos"
      />
    </template>

    <template v-else>
      <li>Нет видео</li>
    </template>
    </div>

  </ul>

  </div>

</template>



<style scoped>
.video-item {
  margin-bottom: 10px;
  list-style: none;
}
.h1{
  color: rgb(89, 0, 0);
  font-style: italic;
  font-size: large;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
  text-align: center;
}
.background{
  background-color: rgb(6, 1, 0);
}
.button{
  color: rgb(6, 1, 0);
  background-color: rgb(118, 114, 115);
  padding: 8px 20;
}
.counter{
  color: rgb(89, 0, 0);
  font-style: italic;
  font-size: large;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  animation-timing-function: cubic-bezier(0.075, 0.82, 0.165, 1);
}
.input {
  display: flex;         /* элементы внутри будут в ряд */
  align-items: center;   /* выравнивание по вертикали */
  gap: 10px;             /* расстояние между input и счетчиком */
  margin-bottom: 15px;   /* небольшой отступ снизу */
}
</style>


