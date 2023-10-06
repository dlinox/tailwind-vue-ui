<template>
  <div
    v-if="showValue"
    @click="emit('update:modelValue', false)"
    class="fixed inset-0 flex items-center justify-center z-50 bg-black/40"
  >
    <slot />
  </div>
</template>
<script setup>
import { computed } from "vue";

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["update:modelValue"]);

const showValue = computed({
  get: () => props.modelValue,
  set: (value) => {
    emit("update:modelValue", value);
  },
});
</script>
