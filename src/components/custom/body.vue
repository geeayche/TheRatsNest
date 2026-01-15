<script setup>
import { ref } from "vue";
import { IMAGES } from "./images";

const showImage = ref(null);
const isMobile = window.innerWidth < 607;
const pages = {
  DRAWINGS: "drawings",
  ABOUT: "about",
  MUSIC: "music",
};
const currentPage = ref(pages.DRAWINGS);

function navigate(page) {
  currentPage.value = page;
}

function setImage(image) {
  showImage.value = image;
}
</script>

<template>
  <link href="src/style.css" rel="stylesheet" />

  <div class="overflow-y-auto">
    <div class="flex justify-center items-start mb-2 md:mb-8 pt-5">
      <span
        class="text-red-500 font-sekuya text-center md:mt-8 text-lg text-wrap md:text-3xl md:text-nowrap cursor-pointer hidden md:block"
        @click="navigate(pages.DRAWINGS)"
        >❄︎♒︎♏︎ ☼︎♋︎⧫︎🕯︎⬧︎ ☠︎♏︎⬧︎⧫︎ (THE RAT'S NEST)</span
      >
      <span
        class="text-red-500 font-sekuya text-center md:mt-8 text-lg text-wrap md:text-3xl md:text-nowrap cursor-pointer block md:hidden"
        @click="navigate(pages.DRAWINGS)"
        >❄︎♒︎♏︎ ☼︎♋︎⧫︎🕯︎⬧︎ ☠︎♏︎⬧︎⧫︎ <br />(THE RAT'S NEST)</span
      >
      <span class="ml-5"
        ><img
          class="cursor-pointer"
          :height="isMobile ? '110px' : '170px'"
          :width="isMobile ? '110px' : '170px'"
          src="../../assets/mainRat.svg"
          @click="navigate(pages.DRAWINGS)"
      /></span>
    </div>

    <div class="flex flex-col">
      <div
        class="grid grid-cols-3 md:grid-cols-5 items-center border-2 border-black"
      >
        <button
          @click="navigate(pages.DRAWINGS)"
          class="items-center md:col-start-2 justify-center p-1 rounded cursor-pointer text-black font-bold underline"
        >
          Drawings
        </button>
        <button
          @click="navigate(pages.MUSIC)"
          class="items-center md:col-start-3 justify-center p-1 rounded cursor-pointer text-black font-bold underline"
        >
          Music
        </button>
        <button
          @click="navigate(pages.ABOUT)"
          class="items-center md:col-start-4 justify-center p-1 rounded cursor-pointer text-black font-bold underline"
        >
          About
        </button>
      </div>

      <div
        v-if="currentPage === pages.ABOUT"
        class="flex flex-col justify-center pt-8"
      >
        <div class="flex flex-col items-center justify-center">
          <img height="450" width="450" src="../../assets/ratKing.svg" />
          <p
            class="flex justify-center mt-10 font-bold text-center text-sm md:text-xl text-black"
          >
            A gathering of drawings, music, and anything else that may come
            about
          </p>
        </div>
      </div>

      <div
        v-if="currentPage === pages.MUSIC"
        class="flex flex-col items-center justify-center pt-8"
      >
        <p
          class="flex justify-center items-center font-bold text-center text-sm md:text-xl text-black"
        >
          Nothing yet
        </p>
      </div>

      <div
        v-if="currentPage === pages.DRAWINGS"
        class="flex flex-col md:pt-10 md:mt-0"
      >
        <div v-if="!isMobile" class="flex flex-col items-center justify-center">
          <img
            class="flex mx-auto h-75 w-75 md:h-150 md:w-150"
            :src="IMAGES[0].source"
          />
          <p
            class="flex mx-auto text-red-500 font-sekuya mt-8 text-center text-sm md:text-xl"
          >
            "{{ IMAGES[0].title }}" - {{ IMAGES[0].date }}
          </p>
          <div class="flex flex-col items-center justify-center mt-20 md:mt-7">
            <p class="underline text-red-500 font-bold text-2xl text-center">
              ========================================================================================================
            </p>
          </div>
        </div>
        <div v-for="n in isMobile ? IMAGES.length : Math.ceil(IMAGES.length / 3)">
          <div class="grid grid-cols-1 md:grid-cols-3">
            <div
              v-for="image in IMAGES.slice(
                isMobile ? n - 1 : (n - 1) * 3,
                isMobile ? n : (n - 1) * 3 + 3
              )"
              :key="image"
              class="flex flex-col mt-5"
            >
              <div class="mt-auto mb-auto">
                <img
                  @click="isMobile ? setImage(null) : setImage(image)"
                  class="flex mx-auto md:cursor-pointer"
                  :height="image.height"
                  :width="image.width"
                  :src="image.source"
                />
              </div>
              <div class="flex flex-col">
                <p
                  class="flex mx-auto text-red-500 font-sekuya mt-4 text-center justify-center text-xs md:text-sm"
                >
                  "{{ image.title }}"
                </p>
                <p
                  class="flex mx-auto text-red-500 font-sekuya mt-4 text-center justify-center text-xs md:text-xs"
                >
                  {{ image.date }}
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="flex flex-col items-center justify-center">
          <p
            class="flex mx-auto text-red-500 mt-10 mb-5 text-center text-sm md:text-xl font-semibold"
          >
            The Rat's Nest 2026
          </p>
        </div>
      </div>

      <div
        v-if="showImage"
        class="absolute inset-0 bg-gray-900 opacity-60"
      ></div>
      <div v-if="showImage" class="absolute inset-0 grid grid-cols-3">
        <div class="invisible">01</div>
        <div class="flex items-center justify-center">
          <img
            :height="showImage.height * 1.5"
            :width="showImage.width * 1.5"
            :src="showImage.source"
          />
        </div>
        <div class="flex align-top justify-end mt-5 mr-15">
          <img
            @click="setImage(null)"
            class="h-10 w-10 cursor-pointer"
            src="../../assets/X.svg"
          />
        </div>
      </div>
    </div>
  </div>
</template>
