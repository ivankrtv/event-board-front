<template>
  <label class="eb-radio">
    {{ props.label }}
    <input
      type="radio"
      class="eb-radio__input"
      :checked="props.modelValue === props.value"
      :value="props.value"
      @change="onChange"
    >
    <span class="eb-radio__trigger" />
  </label>
</template>

<script setup lang="ts">
interface IRadioProps {
  label?: string,
  modelValue?: string | null,
  value: string
}
const props = withDefaults(defineProps<IRadioProps>(), {
  label: '',
  modelValue: null
});

const emit = defineEmits<{
  (e: 'update:modelValue', value: boolean | Object | string): void
}>();

const onChange = (event: InputEvent) => {
  const isChecked = (event.target as HTMLInputElement).checked;
  if (isChecked) {
    emit('update:modelValue', props.value);
  }
};
</script>

<style lang="scss" scoped>
.eb-radio {
  display: block;
  position: relative;
  padding-left: 38px;
  color: $primary-text-color;
  font-size: 1.125rem;
  line-height: 1.375rem;
  cursor: pointer;

  &__input {
    position: absolute;
    opacity: 0;
    height: 0;
    width: 0;
  }

  &__trigger {
    position: absolute;
    top: 0;
    left: 0;
    height: 22px;
    width: 22px;
    background-color: $secondary-background-color;
    border-radius: 8px;
    transition: box-shadow .2s ease-out, background-color .1s ease-in-out;
  }

  &__input:checked ~ &__trigger {
    background-color: $primary-color;
  }

  &:hover &__input:checked ~ &__trigger {
    box-shadow: 0 2px 7px rgba($primary-color, 0.64);
  }
}
</style>

