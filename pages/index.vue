<script setup lang="ts">
const {
  data,
  refresh,
  pending: loading,
  status,
} = useFetch<any>(
  "https://dummyjson.com/comments?limit=10&skip=10&select=body,postId"
);
</script>

<template>
  <main
    class="min-h-screen p-5 flex flex-col justify-center items-center relative"
  >
    <button
      class="absolute top-8 right-8 px-3 py-1 bg-green-700 text-white rounded-md"
      @click="refresh()"
    >
      Refresh
    </button>
    <h1 class="my-3 text-5xl">Comments</h1>

    <section
      v-if="loading"
      class="w-full h-64 flex flex-col justify-center items-center"
    >
      <h1 class="my-3 text-3xl">Loading...</h1>
    </section>

    <ul v-else class="pl-3 my-3">
      <li
        class="text-xl leading-relaxed flex gap-3"
        v-for="item in data?.comments"
        :key="item"
      >
        <span class="text-2xl underline">{{ item?.user.username }}: </span>
        {{ item?.body }}
      </li>
    </ul>
  </main>
</template>

<style scoped></style>
