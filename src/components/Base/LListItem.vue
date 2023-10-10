<template>
  <div
    class="relative w-full   inline-flex justify-between py-2 px-3 items-center"
    :class=" dark ? 'text-white' : 'text-gray-900' "
  >
    <router-link
      v-if="link"
      class="absolute top-0 left-0 w-full h-full"
      :to="href"
    />
    <slot v-if="$slots['prependIcon']" name="prependIcon" />
    <div v-if="prependIcon && !$slots['prependIcon']" class="me-3">
      <LIcon :icon="prependIcon" />
    </div>

    <div class="w-full">
      <div v-if="title" class="text-sm text-ellipsis font-medium">
        {{ title }}
      </div>
      <div v-if="subtitle" class="text-sm text-gray-500">
        {{ subtitle }}
      </div>
      <slot />
    </div>

    <slot v-if="$slots['appendIcon']" name="appendIcon" />

    <div v-if="appendIcon && !$slots['appendIcon']" class="ms-3">
      <LIcon :icon="appendIcon" />
    </div>
  </div>
</template>
<script setup>
import LIcon from "./LIcon.vue";

const props = defineProps({
  title: String,
  subtitle: String,
  prependIcon: String,
  appendIcon: String,
  dark: Boolean,
  link: {
    type: Boolean,
    default: false,
  },
  href: String,
});
</script>
