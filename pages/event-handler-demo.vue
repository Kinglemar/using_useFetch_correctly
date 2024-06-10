<script setup lang="ts">
const data = ref();
const loading = ref(false);
const errorOccured = ref(false);

async function sendData() {
  loading.value = true;
  const { data: apiData, error } = await useFetch(
    "https://dummyjson.com/user/login",
    {
      method: "POST",
      body: user.value,
    }
  );

  if (apiData.value) {
    data.value = apiData.value;
  }
  if (error.value) {
    errorOccured.value = true;
  }
  loading.value = false;
}

async function sendDataUsing$Fetch() {
  try {
    loading.value = true;
    const apiData = await $fetch("https://dummyjson.com/user/login", {
      method: "POST",
      body: user.value,
    });
    console.log(apiData);

    if (apiData) {
      data.value = apiData;
    }
    loading.value = false;
  } catch {
    loading.value = false;
    errorOccured.value = true;
  }
}

const user = ref({
  username: "",
  password: "",
});
</script>

<template>
  <main
    class="min-h-screen p-5 flex flex-col justify-center items-center relative"
  >
    <h1 v-if="!data" class="my-3 text-5xl">Log into your account</h1>
    <h1 v-else class="my-3 text-5xl">Welcome, {{ data?.username }}</h1>

    <section v-if="data">
      <img class="w-36 h-36" :src="data?.image ? data?.image : ''" alt="" />
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
      <p class="text-xl leading-relaxed flex gap-3 mb-4">
        Username:
        <input
          v-model="user.username"
          placeholder="Type username"
          type="text"
          name="username"
          id="username"
          class="border border-blue-800 rounded-md px-3"
        />
      </p>
      <p class="text-xl leading-relaxed flex gap-3">
        Password:
        <input
          v-model="user.password"
          placeholder="Type password"
          type="text"
          name="password"
          id="password"
          class="border border-blue-800 rounded-md px-3"
        />
      </p>
      <p
        v-if="errorOccured"
        class="text-xl leading-relaxed flex gap-3 my-3 text-red-700"
      >
        An error occured.
      </p>
      <button
        @click="sendDataUsing$Fetch"
        class="mt-3 px-3 py-1 bg-blue-800 text-white rounded-md"
      >
        {{ loading ? "Pending.." : "Request access" }}
      </button>
    </section>
  </main>
</template>

<style scoped></style>
