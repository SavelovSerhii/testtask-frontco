<script setup>
  import { onMounted, ref } from 'vue'
  import TheWelcome from './components/TheWelcome.vue';

  const imageList = ref([]);
  const urlList = ref([]);

  function scrollLeft() {
    const lastImage = imageList.value.pop();

    imageList.value.unshift(lastImage);
  }

  function scrollRight() {
    const firstImage = imageList.value.shift();

    imageList.value.push(firstImage);
  }

  function selectImage(url) {
    if (!urlList.value.includes(url)) {
      urlList.value.push(url)
    } else {
      urlList.value.splice(urlList.value.indexOf(url), 1)
    }
  }

  onMounted(() => {
    fetch("https://picsum.photos/v2/list")
      .then((response) => response.json())
      .then((json) => {
        imageList.value = [...json];
      })
  })
</script>

<template>
  <main>
    <TheWelcome :image-list="imageList" :scroll-left="scrollLeft" :scroll-right="scrollRight" :select-image="selectImage" />

    <ul v-if="urlList.length" class="url__list">
      <li class="url__item" v-for="url in urlList" :key="url">
        <a class="url__link" :href="url" target="_blank">{{url}}</a>
      </li>
    </ul>
  </main>
</template>

<style scoped>
  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100%;
  }

  .url__list {
    padding: 16px 24px 16px 48px;
    border: 10px solid burlywood;
    border-top: 0;
    border-bottom-left-radius: 8px;
    border-bottom-right-radius: 8px;
    font-size: 24px;
  }

  .url__link {
    color: rgb(160, 123, 74);
    text-decoration: none;
  }

  .url__link:hover {
    text-decoration: underline;
  }

  @media screen and (max-width: 768px) {
    .url__list {
      padding: 16px 32px;
      font-size: 12px;
    }
  }
</style>
