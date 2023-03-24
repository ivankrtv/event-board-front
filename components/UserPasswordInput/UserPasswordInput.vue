<template>
  <EbTextField
    v-model="password"
    placeholder="Пароль"
    :type="getInputType"
  >
    <template #appendIcon>
      <img
        class="user-password-input__eye-icon"
        :src="getEyeIconSrc"
        alt="toggle password visibility"
        @click="onEyeIconClick"
      >
    </template>
  </EbTextField>
</template>

<script setup lang="ts">
import EbTextField from '~/components/UI/EbTextField/EbTextField.vue';

const password = ref<string>('');
const isPasswordShown = ref<boolean>(false);

const onEyeIconClick = () => {
	isPasswordShown.value = !isPasswordShown.value;
};


import closedEyeIconPath from '~/assets/images/icons/password_eye_closed.svg';
import openedEyeIconPath from '~/assets/images/icons/password_eye_opened.svg';

const getEyeIconSrc = computed(() => {
	return isPasswordShown.value ? closedEyeIconPath : openedEyeIconPath;
});

const getInputType = computed<'text' | 'password'>(() => {
	return isPasswordShown.value ? 'text' : 'password';
});
</script>

<style lang="scss" scoped>
.user-password-input {
	&__eye-icon {
		cursor: pointer;
	}
}
</style>
