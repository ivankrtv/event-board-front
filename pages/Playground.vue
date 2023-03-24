<template>
  <div class="playground">
    <!--    Buttons-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Кнопка secondary</p>
        <EbButton>
          Участовать
        </EbButton>
      </div>

      <div class="playground__element-container">
        <p>Кнопка primary</p>
        <EbButton
          type="primary"
        >
          Участовать
        </EbButton>
      </div>

      <div class="playground__element-container">
        <p>Кнопка disabled secondary</p>
        <EbButton :disabled="true">
          Участовать
        </EbButton>
      </div>

      <div class="playground__element-container">
        <p>Кнопка disabled primary</p>
        <EbButton
          type="primary"
          disabled
        >
          Участовать
        </EbButton>
      </div>
    </div>

    <!--    Text fields-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Текстовое поле</p>
        <EbTextField
          v-model="input"
          placeholder="Имя"
        />
      </div>

      <div class="playground__element-container">
        <p>Пароль</p>
        <UserPasswordInput />
      </div>
    </div>

    <!--    Checkboxes-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Чекбокс</p>
        <EbCheckbox
          v-model="checkbox"
          label="Мафия"
        />
      </div>
    </div>

    <!--    Radios-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Радио</p>
        <EbRadio
          v-model="gender"
          label="Муж"
          :value="genders[0]"
        />
        <EbRadio
          v-model="gender"
          label="Жен"
          :value="genders[1]"
        />
      </div>
    </div>

    <!--		Selects-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Селект</p>
        <EbSelect
          v-model="selectValue"
          placeholder="Выбери общежитие"
          :items="selectItems"
          :display-property="displayProperty"
        />
      </div>
    </div>

    <!--		Hints-->
    <div class="playground__row">
      <div class="playground__element-container">
        <p>Хинты (тултипы) ((подсказки))</p>
        <EbHint :text="hintText" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import EbButton from '~/components/UI/EbButton/EbButton.vue';
import EbTextField from '~/components/UI/EbTextField/EbTextField.vue';
import EbCheckbox from '~/components/UI/EbCheckbox/EbCheckbox.vue';
import EbRadio from '~/components/UI/EbRadio/EbRadio.vue';
import EbSelect from '~/components/UI/EbSelect/EbSelect.vue';
import EbHint from '~/components/UI/EbHint/EbHint.vue';

const input = ref('Канеки Кен');
const checkbox = ref(false);
const gender = ref('female');
const genders = ref(['male', 'female']);
const selectValue = ref(null);
const selectItems = [
	{
		id: 1,
		title: 'Общежитие 19'
	},
	{
		id: 2,
		title: 'Общежитие 1'
	},
	{
		id: 3,
		title: 'Общежитие 6'
	},
	{
		id: 4,
		title: 'Общежитие 6'
	},
	{
		id: 5,
		title: 'Общежитие 6'
	},
	{
		id: 6,
		title: 'Общежитие 6'
	},
];
const displayProperty = (item: any) => item.title;

const hintText = `Почта, которую вам выдал
Политех, например
ivanov.ii@spbstu.edu.ru`;

</script>

<style lang="scss" scoped>
.playground {
  min-width: 100vw;
  width: fit-content;
  height: 100vh;
  overflow-y: scroll;
  padding: 40px 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 40px;
  background-color: $white-color;


  &__row {
    width: fit-content;
    display: grid;
    grid-template-columns: repeat(4, 300px);
    gap: 16px;
  }

  &__element-container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    align-items: flex-start;
  }
}
</style>
