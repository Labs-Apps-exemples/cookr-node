<template>
  <div class="relative">
    <select
      :value="modelValue"
      class="
        appearance-none
        block
        w-full
        overflow-ellipsis
        border border-alt-300
        bg-white
        shadow-inner
        ring-offset-2 ring-offset-alt-100
      "
      :class="{
        'py-3 pl-5 pr-10 rounded-lg': !variant,
        'py-2 pl-2 pr-6 text-sm rounded': variant.includes('small'),
      }"
      v-bind="attrs"
      @input="(e) => $emit('update:model-value', (e.target as HTMLSelectElement).value)"
    >
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
      >
        {{ option.label }}
      </option>
    </select>
    <CIcon
      id="chevron-down"
      class="absolute top-1/2 -mt-3 text-alt-500"
      :class="{
        'right-3': !variant,
        'right-2': variant.includes('small'),
      }"
    />
  </div>
</template>

<script lang="ts">
export type SelectOption = {
  value: string | number;
  label: string;
};
</script>

<script lang="ts" setup>
import { inject, PropType } from 'vue';
import { FormGroupProps } from './FormGroup.vue';

const props = defineProps({
  variant: {
    type: String,
    default: '',
  },
  modelValue: {
    type: [String, Number],
    default: '',
  },
  options: {
    type: Array as PropType<SelectOption[]>,
    default: () => [],
  },
  required: {
    type: Boolean,
    default: null,
  },
});

defineEmits(['update:model-value']);

const formGroup = inject<FormGroupProps | null>('formGroup', null);

const attrs = {
  required: props.required ?? formGroup?.required,
};
</script>
