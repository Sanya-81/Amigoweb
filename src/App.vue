<template>
<div class="g-prt__form--wrapper">
    <form class="g-prt__form">
        <div class="g-chd__form-title">
            <h1 class="h1">Регистрация</h1>
            <p class="access--title">Уже есть аккаунт?<span class="access--check"> Войти</span></p>
        </div>
        <div class="g-chd__form-inputs f-prt__form-input">
            <base-input
                label="Имя"
                placeholder="Введите Ваше имя"
                type="text"
            >
            </base-input>
            <base-input
                label="Email"
                placeholder="Введите Вашу почту"
                type="email"
            >
            </base-input>
            <base-input
                label="Номер телефона"
                placeholder="Введите Ваш телефон"
                type="tel"
            >
            </base-input>
        </div>
        <div class="g-chd__form-select">
        <base-select
            :db='db'
        ></base-select>
        </div>
        <div class="g-chd__form-chekbox" >
            <base-checkbox class="access" @change="check">
                Принимаю <span class="access--check">условия</span> использования
            </base-checkbox>      
        </div>
        <div class="g-chd__form-submit">
            <base-button
                v-if="checked === true"
                class="button"
            >Зарегистрироваться</base-button>
            <base-button
                v-else
                class="button"
                disabled
            >Зарегистрироваться</base-button>
        </div>    
    </form>
</div>
</template>

<script>
import BaseInput    from './components/BaseInput.vue';
import BaseButton   from './components/BaseButton.vue';
import BaseSelect   from './components/BaseSelect.vue';
import BaseCheckbox from './components/BaseCheckbox.vue';
export default {
    components: { 
        BaseInput,
        BaseSelect,
        BaseButton, 
        BaseCheckbox, 
    },
    data() {
        return {
            name: 'App',
            checked: false,
            modelValue: '',
            db: [
                {
                    "value": "E1",
                    "content": "Русский",
                },
                {
                    "value":"E2",
                    "content":"Английский",
                },
                {
                    "value":"E3",
                    "content":"Китайский",
                },
                {
                    "value":"E4",
                    "content":"Испанский",
                },
            ],
        }
    },
    methods: {
        check() {
            this.checked = !this.checked
        }
    }
}
</script>
<style>

    @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@500&display=swap');
    body {
        font-family: 'IBM Plex Sans', sans-serif;
        box-sizing: border-box;
        color: var(--blue800);
        /* background: var(--white); */
    }

    body * {
        box-sizing: inherit;
    }

   
    .g-prt__form--wrapper {
        display: grid;
        height: 100vh;
        align-content: center;
        justify-content: center;
        background-color: var(--grey200);
    }

    .g-prt__form {
        border-radius: 24px;
        padding: 40px 30px;
        display: grid;
        grid: 
            "title" 110px
            "input" auto
            "select" auto
            "checkbox" auto
            "submit" auto
            /minmax(360px, 400px);
        border: 3px solid var(--cyan-blue200);
        background-color: var(--grey0);
        box-shadow: var(--shadowNormal);
    }

    .g-chd__form-title { grid-area: title; }
    .g-chd__form-input { grid-area: input; }
    .g-chd__form-select { grid-area: select; }
    .g-chd__form-chekbox { grid-area: checkbox; }
    .g-chd__form-submit { grid-area: submit; }

    .f-prt__form-input {
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .h1 {
        font-size: 34px;
        margin: 0 0 10px 0;
    }
</style>
<style lang="scss">
  
    .access {
        color: var(--blue800);
    }

    .access--check {
        cursor: pointer;
        color: var(--red600);
    }
    
    .access--title {
        display: inline;
    }

    .validation-message {
        display: block;
        padding-top: 0.4em;
        color: var(--red700);
    }
</style>

