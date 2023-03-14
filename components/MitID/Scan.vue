<script lang="ts" setup>
import { TransitionRoot, TransitionChild } from '@headlessui/vue'


// styles
const styles = reactive<{
  [key: string]: string
}>({
  primary: '',
  success:
    'dark:from-green-500/50 via-gray-200 to-gray-200 dark:via-slate-800 dark:to-slate-800',
  warning:
    'dark:from-yellow-500/50 via-gray-200 to-gray-200 dark:via-slate-800 dark:to-slate-800',
  danger:
    'dark:from-red-500/50 via-gray-200 to-gray-200 dark:via-slate-800 dark:to-slate-800',
})
const textStyles = reactive<{
  [key: string]: string
}>({
  primary: 'text-white',
  success: 'text-green-500',
  warning: 'text-orange-500',
  danger: 'text-red-500',
})
const emit = defineEmits(['scanned'])

const longPollSucces = () => {
  emit('scanned');
}

async function longPoll() {
  let response = await fetch("/verify");

  if (response.status == 502) {
    // Status 502 is a connection timeout error,
    // may happen when the connection was pending for too long,
    // and the remote server or a proxy closed it
    // let's reconnect
    await longPoll();
  } else if (response.status != 200) {
    // An error - let's show it
    console.log(response.statusText);
    // Reconnect in one second
    await new Promise(resolve => setTimeout(resolve, 5000));
    await longPoll();
  } else {
    // Get and show the message
    let message:any = await response.json;
    console.log(message);

    if (message?.response === 'true') {
      longPollSucces();
    } else {
      // Call subscribe() again to get the next message
      await longPoll();
    }
  }
}

longPoll();

</script>

<template>
      <div class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg">
        <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
          <div class="sm:flex sm:items-start">
            <div class="mx-auto flex h-12 w-12 flex-shrink-0 items-center justify-center rounded-full bg-red-100 sm:mx-0 sm:h-10 sm:w-10">
              <svg class="h-6 w-6 text-red-600" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v3.75m-9.303 3.376c-.866 1.5.217 3.374 1.948 3.374h14.71c1.73 0 2.813-1.874 1.948-3.374L13.949 3.378c-.866-1.5-3.032-1.5-3.898 0L2.697 16.126zM12 15.75h.007v.008H12v-.008z" />
              </svg>
            </div>
            <div class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
              <img src="" alt="scan QR image" />
              <!-- long poll -->
            </div>
          </div>
        </div>
      </div>
</template>
