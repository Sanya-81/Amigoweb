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
            v-bind="$attrs"
            @change="isName"
            :type="type"
            :placeholder="placeholder"
            required
            minlength="5"
            id="name"
            name="name"
            aria-describedby="name-validation"
            ref="input"
            @blur ="b"
        ><span 
            id="name-validation" 
            aria-live="assertive" 
            class="validation-message"
            ref='span'
        
        ></span>

            <!-- @invalid="customInValid" -->
            <!-- @valid="customValid" -->
            <!-- :minlength="num()" -->
            <!-- :pattern="regE()" -->
        <br>
        <span
        >{{Err}}</span>
    </p>
    <div id="password-minlength">Enter at lest eignt characters</div>

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
            Err: '',
            reg:{
                "text": '[a-z]{5}',
                "tel":'\\d{4,8}',
            },
        }
    },
    mounted(){
        this.bb()
    },
    methods: {
        bb(){
            const input = this.$refs.input;
            input.setCustomValidity('hello!!!')
        },
        b(e){
            const isValid = e.target.validity.valid;
            console.dir(e.target)
            const message = e.target.validationMessage;
            const connectedValidationId = e.target.getAttribute('aria-describedby');
            const connectedValidation = connectedValidationId 
                ? this.$refs.span
                : false;
            console.log(isValid, message, connectedValidationId, connectedValidation)
            if (connectedValidation && message && !isValid) {
                connectedValidation.innerText = message;
            } else {
                connectedValidation.innerText = '';
            }
        },
       
        customInValid(e){
            const input = e.target;
            console.dir(input)
                input.setCustomValidity('Sanya')
        },
        num(){
            
           return this.type === 'tel' ? 8 : null
        },
        regE(){
            if(this.type === 'tel'){
                console.log('tel')
                return this.reg.tel
            }else if(this.type === 'text'){
                console.log('text')
                return this.reg.text
            }else {
                return null
            }
        },
        isName(e) {
            this.Err = e.target.value;
            
        },
        doText() {
            return  'this is TEXT!'
        },
        doEmail() {
            return 'this is EMAIL!'
        },
        doTel() {
            return  'this is PHONE!'
        }
    },
    watch: {
        Err(){ 
        switch(this.type) {
                case 'text':
                    this.Err = this.doText();
                    break;
                case 'email':
                    this.Err = this.doEmail();
                    break;
                case 'tel':
                    this.Err = this.doTel();
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
