<script lang="ts" setup>
import QrcodeVue from 'qrcode.vue'

// meta
definePageMeta({
  layout: 'page',
})
</script>

<template>
  <PageWrapper>
    <PageBody>
      <div class="bg-white">
        <br><br><br><br><br>

      <PageSection>
          
        <client-only>
          <!--qrcode-vue value="http://localhost:3000" :size="300" level="H" /-->
          <qrcode-vue value="https://mitid.dk" :size="200" level="H" />
  </client-only>
      </PageSection>

      <br><br><br><br>
    </div>      
    </PageBody>
  </PageWrapper>
</template>
