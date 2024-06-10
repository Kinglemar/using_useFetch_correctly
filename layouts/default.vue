<template>
  <main>
    <section class="overflow-hidden relative">
      <section class="inline-flex gap-3 absolute text-xl p-5 top-3 left-3 z-50">
        <NuxtLink to="/"> Home </NuxtLink> |
        <NuxtLink to="/submit"> Submit </NuxtLink> |
        <NuxtLink to="/event-handler-demo"> Event Handler </NuxtLink>
      </section>
      <slot name="default" />
    </section>
  </main>
</template>
