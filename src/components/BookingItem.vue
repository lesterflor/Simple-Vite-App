<script setup>
import { LoaderCircle, Check } from 'lucide-vue-next';
import RoundButton from './RoundButton.vue';
import SectionCard from './SectionCard.vue';
import { computed } from 'vue';

const props = defineProps({
  status: String,
});

const pending = computed(() => props.status === 'pending');
const icon = computed(() => (pending.value ? LoaderCircle : Check));

defineEmits(['cancelled']);
</script>

<template>
  <SectionCard>
    <div class="flex justify-between">
      <slot></slot>
      <div class="flex flex-col-2">
        {{ status }}<component :is="icon" :class="{ 'animate-spin': pending }"></component>
      </div>

      <RoundButton variant="danger" @click="$emit('cancelled')">Cancel</RoundButton>
    </div>
  </SectionCard>
</template>
