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
            minlength="5"
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
        }
    },
    data() {
        return {
            err: '',
            reg:{
                "text": '[a-z]{5}',
                "tel":'\\d{4,8}',
            },
        }
    },
    
    methods: {
        blur(e){
            const input = e.target;
            const inputValid = input.checkValidity();
            const span = this.$refs.span;

            console.log(inputValid)
            console.log(e.target.checkValidity())

            if (!inputValid) {
                this.Error();
                input.setCustomValidity(this.err);
                span.innerText = input.validationMessage;
                input.setCustomValidity('');
            } else {
                span.innerText = '';
            }
        },
       
   
        doText() {
            return  'укажите Ваше имя'
        },
        doEmail() {
            return 'Адрес почты должет иметь "@"'
        },
        doTel() {
            return  'номер телефона должен иметь 11 символов'
        },
        Error(){ 
        switch(this.type) {
                case 'text':
                    this.err = this.doText();
                    break;
                case 'email':
                    this.err = this.doEmail();
                    break;
                case 'tel':
                    this.err = this.doTel();
                    break;
                default:
                    console.log('this is not text or email type')
            }
        }
    }
}
</script>
<style lang="scss">
    .inputLable {
        color: var(--blue800);
    }
    
    .input {
        margin-top: 7px;
        outline: none;
        width: 100%;
        height: 52px;
        padding-left: 16px;
        border-radius: 6px;
        border: 1px solid var(--blue100);
        box-shadow:  var(--shadowNormal);
        background-color: var(--white);
    
        &::placeholder {
            color: var(--blue600);
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
    }
</style>
