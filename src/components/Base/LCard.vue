<template>
  <div class="bg-white max-w-full" :style="`width: ${width} ;`">
    <div
      v-if="$slots['card-header'] || title !== null || subTitle !== null"
      class="p-2 sm:p-3"
    >
      <slot name="card-header" />
      <h3 class="text-base font-semibold leading-7 text-gray-900">
        {{ title }}
      </h3>
      <p class="max-w-2xl text-sm leading-6 text-gray-500">
        {{ subTitle }}
      </p>
    </div>
    <div v-if="$slots['card-body']" class="bg-gray-50 p-3 sm:p-4">
      <slot name="card-body" />
    </div>

    <div v-if="$slots['card-footer']" class="bg-white p-2 sm:p-3">
      <slot name="card-footer" />
    </div>
  </div>
</template>
<script setup>
const props = defineProps({
  variant: {
    type: String,
  },
  loading: {
    type: Boolean,
    default: false,
  },
  title: {
    type: String,
    default: null,
  },
  subTitle: {
    type: String,
    default: null,
  },
  width: {
    type: String,
    default: '100%'
  }
});
</script>
