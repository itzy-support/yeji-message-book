<template>
  <VApp id="messagebook">
    <VAppBar>
      <VAppBarNavIcon @click="drawer = !drawer" />

      <VToolbarTitle>예지에게, 믿지가</VToolbarTitle>

      <VResponsive max-width="108">
        <VTextField
          v-model="visiblePageNumber"
          type="number"
          variant="solo"
          :suffix="`/ ${MAX_PAGE}`"
          hide-details
          flat
        ></VTextField>
      </VResponsive>

      <VBtn icon>
        <VIcon>mdi-dots-vertical</VIcon>
      </VBtn>
    </VAppBar>

    <VNavigationDrawer v-model="drawer">
      <VList :items="index" item-value="page" @click:select="setPage($event)" />
    </VNavigationDrawer>

    <VMain>
      <VCarousel
        v-model="currentPage"
        hide-delimiters
        show-arrows="hover"
        progress="primary"
        height="auto"
      >
        <VCarouselItem
          v-for="(_, index) in pages"
          max-height="93vh"
          :src="`./book/YEJI_MESSAGE_BOOK_${(index + 1)
            .toString()
            .padStart(3, 0)}.jpg`"
        />
      </VCarousel>
    </VMain>
  </VApp>
</template>

<script setup>
import { ref, computed } from "vue";

const drawer = ref(false);
const currentPage = ref(0);
const MAX_PAGE = 182;

const visiblePageNumber = computed({
  get: () => {
    if (currentPage.value < 0) currentPage.value = 0;
    if (currentPage.value > MAX_PAGE) currentPage.value = MAX_PAGE - 1;
    return currentPage.value + 1;
  },
  set: (newValue) => {
    currentPage.value = newValue - 1;
  },
});
const setPage = (index) => {
  currentPage.value = index.id - 1;
};

const pages = new Array(MAX_PAGE);

const index = [
  {
    title: "믿지에게 예지란",
    page: 5,
  },
  {
    title: "예지 vs 옞덩",
    page: 13,
  },
  {
    title: "예지매거진",
    page: 35,
  },
  {
    title: "믿지들이 뽑은 최애 직캠",
    page: 109,
  },
  {
    title: "100문 100답",
    page: 123,
  },
  {
    title: "예지고사",
    page: 137,
  },
  {
    title: "예지로드맵",
    page: 139,
  },
  {
    title: "도전! 예지요리",
    page: 167,
  },
];
</script>
