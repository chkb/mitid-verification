<script lang="ts" setup>
import { capitalize } from '~/utils/str'
import { swipeButton } from 'vue3-swipe-button'

// composable
const { t } = useLang()

// compiler macro
definePageMeta({
  layout: 'page',
})
useHead(() => ({
  title: capitalize(t('pages.blank.title')),
  meta: [
    {
      name: 'description',
      content: t('pages.blank.description'),
    },
  ],
}))


defineNuxtConfig ({
  components: { swipeButton },

  setup() {
    const show = ref(false);
    
    const getButtonColor = computed(() => show.value ? 'purple' : 'green');
    
    const actionMethod = () => show.value = !show.value;

    return { actionMethod, getButtonColor };
  },
})


</script>

<template>
  <PageWrapper>
    <PageHeader>
      <PageTitle text="Godkend med MitID" />
    </PageHeader>
    <PageBody>
      <PageSection>
        <div>
          <input type="checkbox" value="18 Years" checked="true"><label for="vehicle1">&nbsp;I am 18 years</label>
          <input type="checkbox" value="18 Years" checked="true"><label for="vehicle1">&nbsp;</label>
          <input type="checkbox" value="18 Years" checked="true"><label for="vehicle1">&nbsp;I am 18 years</label>



          <swipeButton text="Submit Form"
             @submit="actionMethod" />

        </div>y

      </PageSection>
    </PageBody>
  </PageWrapper>
</template>
