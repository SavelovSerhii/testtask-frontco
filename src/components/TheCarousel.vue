<script setup>
import { onUpdated, ref } from "vue"
  defineProps({
    imageList: Array,
    scrollLeft: Function,
    scrollRight: Function,
    selectImage: Function
  })

  const isMobile = ref(false);

  onUpdated(() => {
    isMobile.value = window.innerWidth <= 768;
  })
</script>

<template>
  <div class="carousel">
    <button class="carousel__button carousel__button--left" v-on:click="scrollLeft">&lt;</button>
    <ul class="carousel__container" v-if="!isMobile">
      <li class="carousel__item" v-for="image in imageList" :key="image" v-on:click="selectImage(image.download_url)">
        <img class="carousel_image" :src="image.download_url" alt="logo">
      </li>
    </ul>

    <ul class="carousel__container" v-if="isMobile">
      <li class="carousel__item" v-on:click="selectImage(imageList[15].download_url)">
        <img class="carousel_image" :src="imageList[15].download_url" alt="logo">
      </li>
    </ul>
    <button class="carousel__button carousel__button--right" v-on:click="scrollRight">&gt;</button>
  </div>
</template>

<style scoped>
  .carousel {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: max-content;
    border-top: 10px solid burlywood;
    border-bottom: 10px solid burlywood;
  }

  .carousel__button {
    position: absolute;
    width: 100px;
    height: 100px;
    font-size: 50px;
    border: 0;
    border-radius: 64px;
    background: #8a8a8a42;
    cursor: pointer;
    transition: all 0.5s;
  }

  .carousel__button:hover {
    color: #ffffff;
    background: #000000c9;
  }

  .carousel__button--left {
    left: 15px;
  }

  .carousel__button--right {
    right: 15px;
  }

  .carousel__container {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 24px;
    margin: 0 130px;
    padding: v-bind(carouselOffset);
    width: 100%;
    list-style: none;
    overflow: hidden;
  }

  .carousel__item {
    display: flex;
    height: 200px;
    cursor: pointer;
  }

  .carousel__item:hover {
    opacity: 75%;
  }

  @media screen and (max-width: 768px) {
    .carousel__button {
      width: 50px;
      height: 50px;
      font-size: 25px;
    }

    .carousel__container {
      margin: 0 80px;
    }

    .carousel__item {
      height: unset;
    }

    .carousel_image {
      width: 100%;
      height: unset;
    }
  }
</style>
