<template>
  <div class="eb-text-field__container">
    <input
      class="eb-text-field"
      :value="props.modelValue"
      :placeholder="props.placeholder"
      :type="type"
      @input="onInput"
    >
    <slot name="appendIcon" />
  </div>
</template>

<script setup lang="ts">
interface ITextFieldProps {
  modelValue?: string | null,
  placeholder: string,
	type?: 'password' | 'text'
}
const props = withDefaults(defineProps<ITextFieldProps>(), {
  modelValue: null,
	type: 'text'
});

const emit = defineEmits<{
  (e: 'update:modelValue', value: string | null): void
}>();

const onInput = (event: InputEvent) => {
  const value = (event.target as HTMLInputElement).value.trim();
  emit('update:modelValue', value.length ? value : null);
};
</script>

<style lang="scss" scoped>
.eb-text-field {
	flex-grow: 1;
  border: none;
  outline: none;

  color: $primary-text-color;
  font-size: 1.125rem;

  &::placeholder {
    color: $light-text-color;
  }

	&__container {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		gap: 24px;
		background-color: $primary-background-color;
		border-radius: 15px;
		padding: 10px 20px;
	}
}
</style>
