<template>
    <div class="wrapper">
        <h1 class="form__title">{{ formTitle }}</h1>
        <!-- Создание каждого нового поля -->
        <div class="field" v-for="(field, index) in fields" :key="index">
            <!-- Если значение field.type равно text, то создаётся текстовое поле -->
            <input v-if="field.type === 'text'" type="text" :placeholder="field.titleText" v-model="field.value" />
            <!-- Если значение field.type равно number, то создаётся числовое поле -->
            <input v-if="field.type === 'number'" type="number" :placeholder="field.titleText" v-model="field.value" :min="field.min" :max="field.max"/>
            <!-- Если значение field.type равно dropdown, то создаётся выпадающий список -->
            <select v-if="field.type === 'dropdown'" v-model="field.value" class="custom-select" :style="field.style" @change="handleChangeList(index, field)">
                <option value="" disabled selected>{{ field.titleText }}</option>
                <option v-for="option in field.options" :key="option" :value="option">{{ option }}</option>
            </select>
        </div>

        <div class="buttons">
            <button class="cancel__btn" @click="cancel">ОТМЕНА</button>
            <!-- Если все поля на ворме заполнены, то кнопке присвается класс submit__btn__active, иначе submit__btn__disabled и на неё нельзя нажать -->
            <button :class="{ 'submit__btn__disabled': isButtonDisabled, 'submit__btn__active': !isButtonDisabled }" @click="submit" :disabled="isButtonDisabled">СОЗДАТЬ</button>
        </div>

    </div>

</template>

<script>
 export default{
    props: {
        fields: Array,
        formTitle: String,
    },
    methods: {
        // Метод для отмены отправки/создания формы
        cancel(){
            console.log("Создание отменено")
        },
        // Метод для отправки/создания формы
        submit(){
            const formData = {
                    fields: this.fields.map(field => ({ name: field.titleName, value: field.value })),
                };
            console.log(formData);
            console.log("Данные отправлены")

        },
        // Метод для стилизации выпадающих списков
        handleChangeList(index, field) {
            field.style = { color: 'black' };
        },
    },
    computed: {
        // Вычислительный метод для проверки, что все поля заполнены
        isButtonDisabled() {
            return this.fields.some(field => !field.value);
        },
    },
 }
</script>

<style scoped>
    *{
        box-sizing: border-box;
        margin: 0;
        font-family: 'Roboto';
    }
    .wrapper{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .form__title{
        margin-top: 1rem;
        font-weight: 400;
        font-size: 1.5rem;
    }
    .field{
        width: 95%;
    }

    input, select{
        font-size: 0.9rem;
        width: 100%;
        height: 50px;
        padding-left: 10px;
        border-radius: 7px;
        background-color: white;
        margin: 1rem 0;
        border: rgba(0,0,0,0.2) solid 1px;
    }

    /* Установка цветов placeholder для текстовых и числовых полей */
    input::-moz-placeholder { color: gray; }
    input::-webkit-input-placeholder { color: gray }

    .custom-select{
        color: gray;
    }
    option:not(:first-child){
        color: black;
    }

    option{
        font-size: 1rem;
        height: 2rem;
    }

    .buttons{
        margin: 1rem 0;
        width: 95%;
        display: flex;
        justify-content: flex-end;
    }

    .buttons>button{
        margin: 0 0.5rem;
        padding: 0 0.5rem;
        font-size: 0.9rem;
        min-width: 6rem;
        min-height: 2rem;
    }

    .cancel__btn{
        color: royalblue;
        font-weight: 700;
        background-color: white;
        border: none;
        letter-spacing: 0.15rem;

    }

    .cancel__btn:hover{
        cursor: pointer;
    }

    .submit__btn__active{
        background-color: rgba(105, 186, 218, 1);
        border-radius: 5px;
        border: none;
        color: white;
        font-weight: 700;
        letter-spacing: 0.15rem;
    }

    .submit__btn__active{
        cursor: pointer;
    }

    .submit__btn__disabled{
        background-color: rgba(187, 205, 211, 1);
        border-radius: 5px;
        border: none;
        color: white;
        font-weight: 700;
        letter-spacing: 0.15rem;
    }

    .submit__btn__disabled{
        cursor: not-allowed;
    }

    .buttons>button:last-child{
        margin-right: 0;
    }
    
</style>