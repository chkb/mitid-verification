<script lang="ts" setup>
definePageMeta({
  layout: 'page',
})
const approved = ref(false);
const swipeClick = async () => {
  const route = useRoute()
   // Default options are marked with *
   const response = await fetch(`https://bystrup.net/mitid-admin-proxy/v1/anonymous/${route.params.sessionId}`, {
    method: "POST", // *GET, POST, PUT, DELETE, etc.
    mode: "cors", // no-cors, *cors, same-origin
    cache: "no-cache", // *default, no-cache, reload, force-cache, only-if-cached
    credentials: "same-origin", // include, *same-origin, omit
    headers: {
      "Content-Type": "application/json",
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: "follow", // manual, *follow, error
    referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    body: JSON.stringify({}), // body data type must match "Content-Type" header
  });
  approved.value = true;
  const res = response.json();
}
</script>

<template>
  <div class="flex justify-center">
    <div class="items-center">
      <img v-if="!approved" style="width: 100vw" @click="swipeClick" src="/swipe.png" alt="" />
      <img v-if="approved" style="width: 100vw"  src="/godkendt.png" alt="" />
    </div>
  </div>
</template>