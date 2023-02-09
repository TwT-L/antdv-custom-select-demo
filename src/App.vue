<script setup>
import CustomOption from './components/CustomOption.vue';
import SvgIcon from './components/svgIcon/SvgIcon.vue';
const options = ref([
  {
    label: '1',
    value: '1',
    svgIcon: 'AD',
  },
  {
    label: '2',
    value: '2',
    svgIcon: 'AE',
  },
  {
    label: '3',
    value: '3',
    svgIcon: 'AF',
  },
]);

const formState = reactive({
  name: '',
  age: undefined,
  country: undefined,
  area: undefined,
});

const containerRef = ref();

const dropdownMatchSelectWidth = ref(true);

const open = ref(false);
const onFocus = () => {
  console.log('focus');
  const newWidth = Math.ceil(containerRef.value.offsetWidth);
  if (dropdownMatchSelectWidth.value !== newWidth) {
    dropdownMatchSelectWidth.value = newWidth;
  }
  open.value = true;
  console.log(newWidth, dropdownMatchSelectWidth.value);
};
const onBlur = () => {
  console.log('blur');
  open.value = false;
};
onMounted(() => {});
</script>

<template>
  <a-form>
    <a-form-item>
      <a-select v-model:value="formState.area" option-label-prop="children">
        <a-select-option v-for="(item, index) in options" :key="index">
          <!-- <div style="display: flex; align-items: center"> -->
          <!-- <SvgIcon
              :name="`countries-${item.svgIcon}`"
              width="26px"
              height="26px"
              style="margin-right: 4px"
            />
            <label for="">{{ item.label }}</label> -->
          <CustomOption
            :iconStyle="{ width: '20px', height: '20px' }"
            :option="item"
          ></CustomOption>
          <!-- </div> -->
        </a-select-option>
      </a-select>
    </a-form-item>
    <a-form-item style="width: 260px; background: red">
      <div ref="containerRef">
        <a-input-number size="large" style="width: 100%">
          <template #addonAfter>
            <a-select
              @focus="onFocus"
              @blur="onBlur"
              :dropdownMatchSelectWidth="dropdownMatchSelectWidth"
              :open="open"
              placement="bottomRight"
              option-label-prop="children"
              @select="onBlur"
              v-model:value="formState.country"
              size="large"
            >
              <!-- <template #option="option">
                <div style="display: flex; align-items: center">
                  <SvgIcon
                    :name="`countries-${option.svgIcon}`"
                    width="26px"
                    height="26px"
                    style="margin-right: 4px"
                  />
                  <label for="">{{ option.label }}</label>
                </div>
              </template> -->
              <a-select-option v-for="(option, index) in options" :key="index">
                <CustomOption
                  :option="option"
                  :iconStyle="{ width: '20px', height: '20px' }"
                />
              </a-select-option>
            </a-select>
          </template>
        </a-input-number>
      </div>
    </a-form-item>
  </a-form>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
