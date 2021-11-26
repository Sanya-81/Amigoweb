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
import BaseButton from './components/BaseButton.vue';
import BaseInput from './components/BaseInput.vue';
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
            ]
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
        background: var(--white);
    }

    body * {
        box-sizing: inherit;
    }

    input[type="checkbox"] {
        -webkit-appearance: none;
        appearance: none;
        display: grid;
        place-content: center;
        background-color: #fff;
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
        box-shadow: inset 1em 1em var(--blue600);
        transform-origin: bottom left;
        clip-path: polygon(15% 50%, 0 50%, 50% 100%, 100% 15%, 90% 0%, 45% 80%);
    }
    
    input[type="checkbox"]:checked::before {
        transform: scale(1);
    }

    input[type="checkbox"]:focus {
        box-shadow: var(--shadowActive);
        outline: none;
    }

    input[type="checkbox"]:hover {
        box-shadow: var(--shadowHover);
    }
 
    :root {
    --number-9: 0.25;
    --number-8: 0.16;
    --number-7: 0.08;
    --number-6: 0.0001;
    --number-5: 0.04;
    --number-4: 0.02;
    
    --white: #ffffff;
    --blue50: #EBF4F8;
    --blue100: #DBE2EA;
    --blue600: #0880AE;
    --blue800: #756F86;
    --blue900: #2C2738;

    --black9: rgba(0, 0, 0, var(--number-9));
    --black8: rgba(44, 39, 56, var(--number-8));
    --black7: rgba(44, 39, 56, var(--number-7));
    --black6: rgba(44, 39, 56, var(--number-6));
    --black5: rgba(44, 39, 56, var(--number-5));
    --black4: rgba(44, 39, 56, var(--number-4));

    --dropShadowButton: 
        drop-shadow(0px 4px 4px var(--black9));
    --dropShadowSelect:
        drop-shadow(0px 4px 8px var(--black5)),
        drop-shadow(0px 20px 20px var(--black5));
    --dropShadowForm:
        drop-shadow(0px 12px 24px var(--black4)),
        drop-shadow(0px 32px 64px var(--black5));
    
    --dropShadowInput: var(--dropShadowSelect);

    --textShadow: 
        0px 4px 4px var(--black9);
    
    --shadowNormal: 
        0px 2px 4px var(--black7), 
        0px 4px 8px var(--black7);
    --shadowHover: 
        0px 12px 24px var(--black7),
        0px 24px 48px var(--black8);
    --shadowActive: 
        0px 2px 4px var(--black6), 
        0px 4px 8px var(--black7);
    
    --shadowBorder: var(--blue600) 0 0 0 2px; 
    }
    
    .g-prt__form--wrapper {
        display: grid;
        height: 100vh;
        align-content: center;
        justify-content: center;
        background-color: var(--blue50);
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
        border: 2px solid var(--blue100);
        background-color: var(--white);
        filter: var(--dropShadowForm);
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
    button {
        appearance: none;
        border: 0;
        border-radius: 0;
        background: none;
        color: inherit;
    }
    .access {
        color: var(--blue800);
    }

    .access--check {
        cursor: pointer;
        color: var(--blue600);
    }
    
    .access--title {
        display: inline;
    }

    .button {
        display: flex;
        justify-content: center;
        align-items: center;
        
        width: 80%;
        min-width: 180px;
        height: 56px;
        margin: 0 auto;
        border-radius: 6px;
        padding-left: 20px;
        padding-right: 20px;
         
        cursor: pointer;
        color: var(--blue50);
        font-family: 'IBM Plex Sans', sans-serif;
        box-shadow: var(--shadowNormal);
        text-shadow: var(--textShadow);
        background-color: var(--blue600);
        
        &:hover {
            text-shadow: none;
            box-shadow: var(--shadowHover);    
            filter: var(--dropShadowButton)
        }

        &:active {
            border: 2px solid var(--blue900);
            box-shadow: var(--shadowActive);    
        }
        
        &:disabled {
            background-color: var(--blue100);
            color: var(--blue900);
            opacity: 0.5;
        }
    }

    // .input {
    //     &:invalid { 
    //        background: #fdd;
    //     }
     
    //     &:valid {
    //         background: #dfd;
    //     } 
    // }

    .validation-message {
        display: block;
        padding-top: 0.4em;
        color: red;
    }
</style>

