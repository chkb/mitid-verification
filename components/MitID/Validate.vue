<script lang="ts" setup>
const emit = defineEmits(['validate'])

const endpoint: string = 'https://bystrup.net/anonymous/v1/anonymous/'
const url: string = `${endpoint}`

const getSessionIdSuccess = (sessionId: string) => {
  emit('validate', sessionId)
}

async function getSessionId() {
  let response = await fetch(url, {
    method: 'POST', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    //credentials: "same-origin", // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json',
      // 'Content-Type': 'application/x-www-form-urlencoded',
    },
    redirect: 'follow', // manual, *follow, error
    //referrerPolicy: "no-referrer", // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
    //body: JSON.stringify(data), // body data type must match "Content-Type" header
  })


  if (response.status === 200) {
    // Get and show the message
    let res: any = await response.json();
    getSessionIdSuccess(res?.sessionId)
  }
}
</script>

<template>
  <div
    class="relative transform overflow-hidden place-content-center rounded-lg bg-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg"
  >
    <div class="mb-8 pt-4 flex flex-col justify-center">
      <div class="self-center">
        <img src="/under18.png" alt="" />
      </div>
      <div>
        <div class="text-gray-900 font-bold text-xl mb-2">Age verfication</div>
        <p class="text-gray-700 text-base">
          This site contains content that is unsuitable for individuals under
          the age of 18, therfore you need to validate your age.
        </p>
      </div>
      <div class="pt-8">
        <button
          @click="getSessionId()"
          type="button"
          class="inline-flex w-full justify-center rounded-md bg-white border px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-500 sm:ml-3 sm:w-auto"
        >
          <img src="/mitid.png" width="50" alt="" />
        </button>
      </div>
    </div>
  </div>
</template>
