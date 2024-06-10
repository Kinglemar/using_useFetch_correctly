<script setup lang="ts">
type User = {
  id: number;
  email: string;
  username: string;
  firstName: string;
  gender: string;
  image: string;
  lastName: string;
  refreshToken: string;
  token: string;
};

const userCredentials = ref({
  username: "emilys",
  password: "emilyspass",
});

const {
  data,
  execute,
  pending,
  error,
  status,
} = useFetch<User>("https://dummyjson.com/user/login", {
  method: "POST",
  body: userCredentials.value,
  immediate: false,
  lazy: true,
});
</script>

<template>
  <main
    class="min-h-screen p-5 flex flex-col justify-center items-center relative"
  >
    <h1 v-if="!data" class="my-3 text-5xl">Log into your account</h1>
    <h1 v-else class="my-3 text-5xl">Welcome, {{ data?.username }}</h1>

    <section v-if="data">
      <img class="w-36 h-36" :src="data.image ? data?.image : ''" alt="" />
      <p class="text-xl leading-relaxed flex gap-3">
        Gender: {{ data?.gender }}
      </p>
      <p class="text-xl leading-relaxed flex gap-3">
        First Name: {{ data?.firstName }}
      </p>
      <p class="text-xl leading-relaxed flex gap-3">
        Last Name: {{ data?.lastName }}
      </p>
    </section>

    <section v-else class="w-fit h-full">
      <p class="text-xl leading-relaxed flex gap-3">
        Username: {{ userCredentials?.username }}
      </p>
      <p class="text-xl leading-relaxed flex gap-3">
        Password: {{ userCredentials?.password }}
      </p>
      <button
        @click="() => execute()"
        class="mt-3 px-3 py-1 bg-green-700 text-white rounded-md"
      >
        {{ pending ? "Request access" : "Pending.." }}
      </button>
    </section>
  </main>
</template>

<style scoped></style>
