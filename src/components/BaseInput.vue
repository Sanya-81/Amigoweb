<template>
<div>
    <p>
        <label class="inputLable">{{label}}</label>
        <br>
        <!-- <input
            class="input"
            v-bind="$attrs"
            :placeholder="placeholder"
            :value="modelValue"
            @input="$emit('update:modelValue', $event.target.value)"
            :type="type"
        >
        <br> -->
        <input
            class="input"
            ref="input"
            v-bind="$attrs"
            @blur ="blur"
            :type="type"
            :placeholder="placeholder"
            required
            :pattern="pattern"
            id="name"
            name="name"
            aria-describedby="name-validation">
        <span 
            ref='span'
            id="name-validation" 
            aria-live="assertive" 
            class="validation-message">
        </span>
        <br>
    </p>

</div>
</template>

<script>
export default {
    inheritAttrs: false,
    emits: ['update:modelValue'],
    props: {
        label: {
            type: String,
            default:'',
        },
        placeholder: {
            type: String,
            default: '',
        },
        modelValue: {
            type: String,
            default: '',
        },
        type: {
            type: [String, Number],
            default: '',
        },
    },
    data() {
        return {
            err: '',
            pattern: '',
            regular:{
                "text": "[A-Za-zА-ЯЁа-яё]{3,}",
                "tel": "[0-9]{11}",
                "email": ".+@.+\\..+"
            },
        }
    },

    created(){
        // заполняет pattern для input и подготавливает строку для ошибки
        this.initValidation()
    },
    
    methods: {
        blur(e){
            const input = e.target;
            const inputValid = input.checkValidity();
            const span = this.$refs.span;

            if (!inputValid) {
                // this.initValidation();
                input.setCustomValidity(this.err);
                span.innerText = input.validationMessage;
                input.setCustomValidity('');
            } else {
                span.innerText = '';
            }
        },
       
        RegExp(type) {
            console.log(this.regular[type])
            return this.regular[type]
        },

        doText() {
            return  'Имя должно быть более 3 букв и не должно содержать цифр, символов, пробелов'
        },
        doEmail() {
            return 'Почта должна заполненна корректно. присутствие символа "@" обязательно '
        },
        doTel() {
            return  'номер телефона должен содержать 11 символов'
        },
        initValidation(){ 
        switch(this.type) {
                case 'text':
                    this.pattern = this.RegExp(this.type);
                    this.err = this.doText(this.type);
                    break;
                case 'email':
                    this.pattern = this.RegExp(this.type);
                    this.err = this.doEmail(this.type);
                    break;
                case 'tel':
                    this.pattern = this.RegExp(this.type);
                    this.err = this.doTel(this.type);
                    break;
                default:
                    console.log('this is not text or email type')
            }
        }
    }
}
</script>
<style lang="scss">
    
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
    
    .input {
        margin-top: 7px;
        outline: none;
        width: 100%;
        height: 52px;
        padding-left: 16px;
        border-radius: 6px;
        border: 1px solid var(--blue200);
        box-shadow:  var(--shadowNormal);
    
        &::placeholder {
            color: hsl( 0, 100%, 80%);
        }

        &:focus {
            box-shadow:
                var(--shadowBorder),
                var(--shadowActive);

        }
        &:hover {
            box-shadow: 
                var(--shadowBorder), 
                var(--shadowHover);
        }

        &:invalid { 
            background-color: hsl( 0, 100%, 98%);
        }
     
        &:valid {
            background: var(--green100);
        } 
    }

    .inputLable {
        color: var(--blue-magenta600);
    }

</style>
