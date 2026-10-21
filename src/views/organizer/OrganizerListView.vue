<script setup lang="ts">
import type { Organizer } from '@/types'
import { ref, onMounted } from 'vue'
import OrganizerService from '@/services/OrganizerService'
import { useRouter } from 'vue-router'

const organizers = ref<Organizer[]>([])
const router = useRouter()

onMounted(() => {
  OrganizerService.getOrganizers()
    .then((response) => {
      organizers.value = response.data
    })
    .catch(() => {
      router.push({ name: 'network-error-view' })
    })
})
</script>

<template>
  <h1>Organizers</h1>
  <div class="flex flex-col items-center">
    <div
      v-for="organizer in organizers"
      :key="organizer.id ?? undefined"
      class="p-5 w-[250px] border border-[#39495c] mb-[18px]"
    >
      <h2>{{ organizer.organizationName }}</h2>
      <span>{{ organizer.address }}</span>
    </div>
  </div>
</template>
