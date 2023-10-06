<template>
  <span
    :class="` ${classDensity[density]}
    ${
      variant === 'flat'
        ? `bg-${color}-500 text-white ring-1 ring-inset ring-${color}-500/10`
        : variant === 'tonal'
        ? `bg-${color}-50 text-${color}-500 ring-1 ring-inset ring-${color}-500/10 `
        : variant === 'text'
        ? `text-${color}-500`
        : variant === 'outlined'
        ? `border border-${color}-500 text-${color}-500 border-solid ring-1 ring-inset ring-${color}-500/10`
        : `bg-${color}-50 text-${color}-500`
    }

    rounded-${rounded}
    `"
    class="font-medium"
  >
    {{ text }}
  </span>
</template>
<script setup>
import { ref } from "vue";

const props = defineProps({
  density: {
    type: String,
    default: "sm",
  },
  color: {
    type: String,
    default: "blue",
  },
  rounded: {
    type: String,
    default: "md",
  },
  variant: {
    type: String,
    default: "flat",
  },
  text: {
    type: String,
    default: "default",
  },
  icon: {
    type: String,
    default: null,
  },
});

const classDensity = ref({
  sm: "px-2 py-1 text-xs",
  md: "px-2.5 py-1.5 text-sm",
  lg: "px-3 py-2 text-md",
  xl: "px-3.5 py-2.5 text-lg",
});

// const classVariant = computed(() => ({
//   flat: `bg-${props.color}-500 text-white`,
//   tonal: `bg-${props.color}-50 text-${props.color}-500`,
//   text: `text-${props.color}-500`,
//   outlined: `border border-${props.color}-500 text-${props.color}-500 border-solid`,
// }));
</script>
