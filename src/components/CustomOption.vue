<template>
  <div class="custom-option">
    <template v-if="option.icon || option.svgIcon">
      <span
        v-if="option.icon"
        role="img"
        :aria-label="option[optionLabelProps.value]"
        class="option-img-wrap"
      >
        <img class="option-img" :src="option.icon" alt="" />
      </span>
      <SvgIcon
        v-else
        class="svg-icon"
        :name="`countries-${option.svgIcon}`"
        :style="iconStyle"
      />
      <span class="option-label">{{ option[optionLabelProps.label] }}</span>
      <small class="option-desc">{{ option[optionLabelProps.desc] }}</small>
    </template>
    <template v-else>{{ option[optionLabelProps.label] }}</template>
  </div>
</template>

<script setup>
import SvgIcon from './svgIcon/SvgIcon.vue';
const props = defineProps({
  option: {
    type: Object,
    default: () => ({}),
  },
  iconStyle: {
    type: Object,
    default: () => ({}),
  },
  optionLabelProps: {
    type: Object,
    default: () => ({
      label: 'label',
      value: 'value',
      desc: 'desc',
    }),
  },
});

onMounted(() => {
  setTimeout(() => {
    console.log(props.option);
  }, 2000);
});
</script>
<style lang="less" scoped>
.custom-option {
  display: flex;
  column-gap: 10px;
  align-items: center;
  .option-img-wrap,
  .svg-icon {
    flex-basis: 22px;
    width: 22px;
  }
  .svg-icon {
    font-size: 26px;
  }
  .option-desc {
    margin-left: 10px;
  }
}
</style>
