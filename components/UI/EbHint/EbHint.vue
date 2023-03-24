<template>
  <div class="eb-hint">
    <img
      src="~/assets/images/icons/hint_question.svg"
      alt="hint"
      class="eb-hint__icon"
    >
    <div class="eb-hint__text">
      {{ props.text }}
    </div>
  </div>
</template>

<script setup lang="ts">
interface IHintProps {
	text: string;
}

const props = defineProps<IHintProps>();
</script>

<style lang="scss" scoped>
.eb-hint {
	position: relative;
	width: 20px;
	height: 20px;
	&:hover .eb-hint__text {
		display: block;
	}

	&__icon {
		cursor: pointer;
	}

	&__text {
		position: absolute;
		display: none;
		top: 50%;
		left: 50%;
		padding: 8px;
		border-radius: 10px;
		background-color: $third-background-color;
		color: $white-color;
		font-size: 1.125rem;
		line-height: 1.125rem;
		max-width: 220px;
		animation: hint .3s;
	}
}

@keyframes hint {
	from {
		opacity: 0;
	}

	to {
		opacity: 1;
	}
}
</style>
