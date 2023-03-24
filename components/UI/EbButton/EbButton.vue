<template>
  <button
    class="eb-button"
    :class="getButtonClasses"
    :disabled="props.disabled"
    @click="onClick"
  >
    <slot />
  </button>
</template>

<script setup lang="ts">
  interface IButtonProps {
    type?: 'primary' | 'secondary',
    disabled?: boolean,
  }
  const props = withDefaults(defineProps<IButtonProps>(), {
    type: 'secondary',
    disabled: false,
  });

  const emit = defineEmits<{
    (e: 'click'): void
  }>();

  const onClick = () => emit('click');

  const getButtonClasses = computed(() => {
    return {
      'eb-button--primary': props.type === 'primary',
      'eb-button--secondary': props.type === 'secondary',
      'eb-button--disabled': props.disabled,
    };
  });
</script>

<style lang="scss" scoped>
.eb-button {
  padding: 10px 12px;
  border-radius: 15px;
  border: none;
  cursor: pointer;
  color: $white-color;
  font-size: 1.125rem;
  transition: box-shadow .2s ease-out;
	&:focus {
		outline: none;
	}

  &--primary {
    background-color: $primary-color;
    &:hover:not(:disabled) {
      box-shadow: 0 3px 13px rgba($primary-color, 0.6);
    }
  }
  &--secondary {
    background-color: $secondary-color;
    &:hover:not(:disabled) {
      box-shadow: 0 3px 13px rgba($secondary-color, 0.6);
    }
  }

  &--disabled {
    opacity: .7;
    cursor: default;
  }
}
</style>
