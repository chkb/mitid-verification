<template>
  <div
    class="relative transform overflow-hidden place-content-center rounded-lg bg-white shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg"
  >
      <div class="mb-8 pt-4 flex flex-col justify-center">
        <div class="self-center">
          <img src="/under18.png" alt="" />
        </div>
        <div>
          <div class="text-gray-900 font-bold text-xl mb-2">
           Age verfication
          </div>
          <p class="text-gray-700 text-base">
           This site contains content that is unsuitable for individuals under the age of 18, therfore you need to validate your age.
          </p>
        </div>
        <div class="pt-8">
          <button
          @click="$emit('validate')"
          type="button"
          class="inline-flex w-full justify-center rounded-md bg-white border px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-500 sm:ml-3 sm:w-auto"
          >
          <img src="/mitid.png" width="50" alt="" />
        </button>
        </div>
    </div>
  </div>
</template>
