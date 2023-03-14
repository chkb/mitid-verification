<script lang="ts" setup>
const endpoint: string = 'https://bystrup.net/anonymous/v1/anonymous/'

const props = defineProps({
  sessionId: String,
})
const url: string = `${endpoint}${props.sessionId}`
const emit = defineEmits(['scanned'])

const longPollSucces = () => {
  emit('scanned')
}

async function longPoll() {
  let response = await fetch(url)

  if (response.status == 502) {
    // Status 502 is a connection timeout error,
    // may happen when the connection was pending for too long,
    // and the remote server or a proxy closed it
    // let's reconnect
    await longPoll()
  } else if (response.status != 200) {
    // An error - let's show it
    console.log(response.statusText)
    // Reconnect in one second
    await new Promise((resolve) => setTimeout(resolve, 2000))
    await longPoll()
  } else {
    // Get and show the message
    let message: any = await response.json()
    if (message?.response) {
      longPollSucces()
    } else {
      // Call subscribe() again to get the next message
      await longPoll()
    }
  }
}

longPoll()
</script>

<template>
  <div
    class="relative transform overflow-hidden rounded-lg bg-white text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-lg"
  >
    <div class="bg-white px-4 pt-5 pb-4 sm:p-6 sm:pb-4">
      <img src="/mitid.png" width="50" alt="" />
      <MitIDQR :sessionId="props.sessionId" />
    </div>
  </div>
</template>
