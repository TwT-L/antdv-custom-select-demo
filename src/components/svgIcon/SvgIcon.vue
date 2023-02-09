<template>
  <svg aria-hidden="true">
    <use :href="symbolId" :fill="color"></use>
  </svg>
</template>
<script setup>
const props = defineProps({
  prefix: {
    type: String,
    default: 'svg',
  },
  name: {
    type: String,
    required: true,
  },
  color: {
    type: String,
    default: undefined,
  },
});

const symbolId = computed(() => `#${props.prefix}-${props.name}`);
</script>
