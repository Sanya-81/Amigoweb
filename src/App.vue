<template>
<div class="g-prt__form--wrapper">
    <form class="g-prt__form">
        <div class="g-chd__form-title">
            <h1 class="h1">Регистрация</h1>
            <p class="access--title">Уже есть аккаунт?<span class="access--check"> Войти</span></p>
        </div>
        <div class="g-chd__form-inputs f-prt__form-input">
            <BaseInput
                label="Имя"
                placeholder="Введите Ваше имя"
                type="text"
            >
            </BaseInput>
            <BaseInput
                label="Email"
                placeholder="Введите Вашу почту"
                type="email"
            >
            </BaseInput>
            <BaseInput
                label="Номер телефона"
                placeholder="Введите Ваш телефон"
                type="tel"
            >
            </BaseInput>
        </div>
        <div class="g-chd__form-select">
        <BaseSelect
            :db='db'
        ></BaseSelect>
        </div>
        <div class="g-chd__form-access">
            <p class="f-prt__form-access access">
                <input name="check" id="check" type="checkbox" v-model="checked">
                <label for="check" >Принимаю <span class="access--check">условия</span> использования</label>
            </p>
        </div>
        <div class="g-chd__form-submit">
            <BaseButton
                v-if="checked === true"
                class="button"
            >Зарегистрироваться</BaseButton>
            <BaseButton
                v-else
                class="button"
                disabled
            >Зарегистрироваться</BaseButton>
        </div>    
    </form>
</div>
</template>

<script>
import BaseInput from './components/BaseInput.vue';
import BaseButton from './components/BaseButton.vue';
import BaseSelect from './components/BaseSelect.vue';
export default {
    components: { 
        BaseButton, 
        BaseInput,
        BaseSelect, 
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

    input[type="checkbox"] {
        -webkit-appearance: none;
        appearance: none;
        display: grid;
        place-content: center;
        background-color: var(--grey0);
        margin: 0;
        font: inherit;
        color: currentColor;
        width:  28px;
        height: 28px;
        border: 0.15em solid currentColor;
        border: 0.15em solid var(--blue600);
        border-radius: 4px;
    }

    input[type="checkbox"]::before {
        content: "";
        width:  16px;
        height: 16px;
        transform: scale(0);
        transition: 120ms transform ease-in-out;
        /* box-shadow: inset 2px 2px var(--cyan600); */
        transform-origin: center;
        background: var(--green-cyan700);
        /* transform-origin: bottom left; */
        /* clip-path: polygon(15% 50%, 0 50%, 50% 100%, 100% 15%, 90% 0%, 45% 80%); */
    }
    
    input[type="checkbox"]:checked::before {
        transform: scale(1);
    }

    input[type="checkbox"]:focus {
        box-shadow: var(--shadowNormal);
        outline: none;
    }

    input[type="checkbox"]:hover {
        box-shadow: var(--shadowHover);
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
            "access" auto
            "submit" auto
            /minmax(360px, 400px);
        border: 3px solid var(--cyan-blue200);
        background-color: var(--grey0);
        box-shadow: var(--shadowNormal);
    }

    .g-chd__form-title { grid-area: title; }
    .g-chd__form-input { grid-area: input; }
    .g-chd__form-select { grid-area: select; }
    .g-chd__form-access { grid-area: access; }
    .g-chd__form-submit { grid-area: submit; }

    .f-prt__form-access {
        display: flex;
        align-items: center;
        gap: 8px;
    }

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

