<template>
  <div
    v-click-outside="onOutsideClick"
    class="eb-select"
  >
    <div
      class="eb-select__trigger"
      @click="onTriggerClick"
    >
      <p
        v-if="props.modelValue"
        class="eb-select__selected-value"
      >
        {{ props.displayProperty(props.modelValue) }}
      </p>
      <p
        v-else
        class="eb-select__placeholder"
      >
        {{ props.placeholder }}
      </p>
      <img
        class="eb-select__arrow"
        :class="getArrowClass"
        src="~/assets/images/icons/select_arrow.svg"
        alt="open select"
      >
    </div>
    <ul
      v-if="isOpen"
      class="eb-select__options-list"
    >
      <li
        v-for="(item, index) in props.items"
        :key="index"
        class="eb-select__option"
        @click="onOptionClick(item)"
      >
        {{ props.displayProperty(item) }}
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
interface ISelectProps {
  placeholder: string;
  modelValue?: string | Object | null;
	items: Array<any>;
	displayProperty?: (item: any) => string;
}
const props = withDefaults(defineProps<ISelectProps>(), {
  modelValue: null,
	displayProperty: (item: any) => item
});

const emit = defineEmits<{
	(e: 'update:modelValue', value: any): void
}>();

const isOpen = ref<boolean>(false);

const onOptionClick = (item: any) => {
  emit('update:modelValue', item);
	isOpen.value = false;
};

const getArrowClass = computed(() => {
	return {
		'eb-select__arrow--rotated': isOpen.value
	};
});

const onTriggerClick = () => isOpen.value = !isOpen.value;
const onOutsideClick = () => isOpen.value = false;
</script>

<style lang="scss" scoped>
.eb-select {
	width: 100%;
  position: relative;

  &__trigger {
    display: flex;
    justify-content: space-between;
    gap: 32px;
    user-select: none;
    cursor: pointer;
    border-radius: 15px;
    background-color: $primary-background-color;
    padding: 8px 16px;
  }
	&__selected-value {
		font-size: 1.125rem;
		color: $primary-text-color;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
  &__placeholder {
    font-size: 1.125rem;
    color: $secondary-text-color;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  &__options-list {
    width: 100%;
    max-height: 168px;
    position: absolute;
    top: calc(100% + 2px);
    left: 0;
    border-radius: 15px;
    background-color: $primary-background-color;
    overflow-y: scroll;
    list-style: none;
		z-index: 2;

		&::-webkit-scrollbar-track {
			border-top-right-radius: 15px;
			border-bottom-right-radius: 15px;
		}
  }
  &__option {
		color: $primary-text-color;
    padding: 8px 16px;
    transition: background-color .1s ease-in-out;
    &:hover {
      background-color: $secondary-background-color;
    }
    cursor: pointer;
  }
	&__arrow {
		transition: transform .2s ease-in-out;
		&--rotated {
			transform: rotateZ(180deg);
		}
	}
}
</style>
