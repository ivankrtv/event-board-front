<template>
  <label class="eb-checkbox">
    {{ props.label }}
    <input
      type="checkbox"
      class="eb-checkbox__input"
      :checked="props.modelValue"
      @change="onChange"
    >
    <span class="eb-checkbox__trigger" />
  </label>
</template>

<script setup lang="ts">
interface ICheckboxProps {
  label?: string,
  modelValue?: boolean,
}
const props = withDefaults(defineProps<ICheckboxProps>(), {
  label: '',
  modelValue: false
});

const emit = defineEmits<{
  (e: 'update:modelValue', value: boolean): void
}>();

const onChange = (event: InputEvent) => {
  const value = (event.target as HTMLInputElement).checked;
  emit('update:modelValue', value);
};
</script>

<style lang="scss" scoped>
.eb-checkbox {
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
