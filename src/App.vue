<template>

  <CreateForm class="create__form" :formTitle="formTitle" :fields="fields"/>

</template>

<script>
import CreateForm from './components/CreateForm.vue';

export default {
  name: 'App',
  components: {
    CreateForm,
  },
  data() {
    return {
      // Массив объектов, который передаётся в форму, который состоит из titleName (Имя поля), titleText (Название поля), 
      // type (Тип поля [text, number, dropdown]), options (Перечисление элементов выподающего списка), 
      // min max (минимальное и максимальное значения числового поля), value (значение)
      fields: [
        {titleName: 'employee', titleText: 'Сотрудник', type: 'dropdown', options: ['Петров Иван Сергеевич', 'Васильченко Дмитрий Васильевич', 'Сухорукова Ирина Михайловна'], value: ''},
        {titleName: 'headEmployee', titleText: 'Руководитель сотрудника', type: 'dropdown', options: ['Петров Иван Сергеевич', 'Васильченко Дмитрий Васильевич', 'Сухорукова Ирина Михайловна'], value: ''},
        {titleName: 'betType', titleText: 'Тип ставки', type: 'dropdown', options: ['opex', 'capex'], value: ''},
        {titleName: 'businessUnit', titleText: 'Бизнес-единица', type: 'dropdown', options: ['MVM', 'MTech'], value: ''},
        {titleName: 'capPercentage', titleText: 'Процент капитализации', type: 'number', min: 0, max: 100, value: ''},
        {titleName: 'jobTitle', titleText: 'Должность', type: 'text', value: ''},
      ],
      // Название формы
      formTitle: "Создание"

    };
  }
}
</script>

<style>
  .create__form{
    width: 30%;
    border-radius: 7px;
    border: 2px solid rgba(0, 0, 0, 0.4);
    margin: 0 auto;
  }
</style>
