<script lang="ts" setup>
import QrcodeVue from 'qrcode.vue'

// meta
definePageMeta({
  layout: 'page',
})

const endpoint:string = "https://main--sparkling-empanada-bf1681.netlify.app/approve/";

const props = defineProps({
  sessionId: String
})


const url:string = `${endpoint}${props.sessionId}`
</script>

<template>
  <PageWrapper>
    <PageBody>
      <div class="bg-white">
        <br><br><br><br><br>

      <PageSection>
          
        <client-only>
          <qrcode-vue :value="url" :size="300" level="H" />
        </client-only>
      </PageSection>

      <br><br><br><br>
    </div>      
    </PageBody>
  </PageWrapper>
</template>
