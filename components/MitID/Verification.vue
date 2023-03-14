<script lang="ts" setup>
import { TransitionRoot, TransitionChild } from '@headlessui/vue'
import Validate from './Validate.vue'
import Scan from './Scan.vue'
import Result from './Result.vue'
export type IStyles = 'primary' | 'success' | 'warning' | 'danger'

// props
const props = defineProps({
  title: {
    type: String,
    default: undefined,
  },
  text: {
    type: String,
    default: undefined,
  },
  type: {
    type: String,
    default: 'primary',
  },
})


enum components {
  validate,
  scan,
  result

}

const componentState = ref(components.validate)

const switchContentEnum = (newState:components) => {
  componentState.value = newState;
}

const validate = () => {
  console.log("Hey validate");
  switchContentEnum(components.scan);
};


</script>

<template>
<div class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
  <!--
    Background backdrop, show/hide based on modal state.

    Entering: "ease-out duration-300"
      From: "opacity-0"
      To: "opacity-100"
    Leaving: "ease-in duration-200"
      From: "opacity-100"
      To: "opacity-0"
  -->
  <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>

  <div class="fixed inset-0 z-10 overflow-y-auto">
    <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
      <Validate @validate="validate" v-if="componentState==components.validate" />
      <Scan v-if="componentState==components.scan" />
      <Result v-if="componentState==components.result" />
    </div>
  </div>
</div>
</template>
