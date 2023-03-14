<script lang="ts" setup>
import Validate from './Validate.vue'
import Scan from './Scan.vue'
import Result from './Result.vue'
export type IStyles = 'primary' | 'success' | 'warning' | 'danger'


const dialogOpen = ref(true);
const sessionIdObject = ref({sessionId : ''});

enum components {
  validate,
  scan,
  result
}

const componentState = ref(components.validate)

const switchContentEnum = (newState:components) => {
  componentState.value = newState;
}

const validate = (sessionId: string) => {
  sessionIdObject.value.sessionId = sessionId;
  switchContentEnum(components.scan);
};

const closeDialog = () => {
  dialogOpen.value = false;
};

const scanned = () => {
  setTimeout(() =>{
    closeDialog()
  },3000)
  switchContentEnum(components.result);
};
</script>

<template>
<div v-if="dialogOpen" class="relative z-10" aria-labelledby="modal-title" role="dialog" aria-modal="true">
  <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity"></div>
  <div class="fixed inset-0 z-10 overflow-y-auto">
    <div class="flex min-h-full items-end justify-center p-4 text-center sm:items-center sm:p-0">
      <Validate @validate="validate" v-if="componentState==components.validate" />
      <Scan @scanned="scanned" :sessionId="sessionIdObject.sessionId" v-if="componentState==components.scan" />
      <Result v-if="componentState==components.result" />
    </div>
  </div>
</div>
</template>
