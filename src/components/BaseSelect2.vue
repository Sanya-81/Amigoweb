<template>
<div>
    <span class="selectLabel" id="jobLabel">Main job role</span>
    <div class="selectWrapper">
        <select class="selectNative js-selectNative" aria-labelledby="jobLabel"
                @change= changeNative($event)
                ref='native'
        >
            <option 
                value="sel"         
                disabled 
                selected
                ref="option"
            > {{elSelectNative}}</option>
            <option 
                v-for = "obj of db"
                :key  = "obj.value"
                :value = obj.value
            >{{obj.content}}</option>    
            
        </select>
        <div 
            :class="{isActive: Active}"
            class="selectCustom js-selectCustom" 
            :aria-hidden = ariaHidden
        ><div
            @click = openSelectCustom()
            class="selectCustom-trigger"
                ref='closeSelectRoot'
            > {{elSelectNative}}</div>
            <div 
                class="selectCustom-options"
            >
                <div
                    v-for = "(obj,index) of db"
                    :key  = obj.value
                    :class="[
                        {isActive: elSelectNative === obj.content}, {isHover: optionChecked === obj.value}
                    ]"
                    class = "selectCustom-option"
                    :data-value = obj.value
                    @mouseenter = "
                        optionChecked = obj.value, 
                        optionIndex = index
                    "
                    @click = "
                        elSelectNative = obj.content, 
                        changeCustom($event),
                        closeSelectCustom()
                    "
                >{{obj.content}}</div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    props: {
        db: {
            type: Array,
        }
    },
    data() {
        return {
            Active: false,
            ariaHidden: 'true',
            optionChecked: null,
            optionIndex: -1,
            value: '',
            content: '',
            'data-value': '',
            elSelectNative: 'Select role...',
        }
    },
    
    methods: {
        changeNative(event) {
            const nativeValue = event.target.value;
            const proxy = this.db.filter((obj, index) => {
                this.optionIndex = index;
                return obj.value === nativeValue}); 
            this.elSelectNative =  proxy[0].content
            this.optionChecked = nativeValue
        },

        changeCustom(event) {
            this.$refs.native.value = event.target.getAttribute("data-value")
            console.log(event.target)
        },

        openSelectCustom() {
            this.Active = !this.Active
            this.ariaHidden = 'false';
        },

        closeSelectCustom() {
            this.ariaHidden = 'true';
            this.Active = false
        },
        
        closeSelectRoot(e) {
            const el = this.$refs.closeSelectRoot;
            const target = e.target;
            if  (el != target && !el.contains(target)) {
                this.Active = false
            }
        },
        
        currentOptionValue() {
            const optionValue = this.db[this.optionIndex].value
            this.optionChecked = optionValue
        },

        KeyboardNavigation(e) {
            if(this.Active && e.keyCode === 40){
                e.preventDefault();
                
                if(this.optionIndex != this.db.length - 1){
                    this.optionIndex++;
                    this.currentOptionValue();
                } 
            }

            if(this.Active && e.keyCode === 38){
                e.preventDefault();
                
                if(this.optionIndex > 0){
                    this.optionIndex--;
                    this.currentOptionValue();
                }
            }

            if(this.Active && e.keyCode === 13 || e.keyCode === 32){
                this.$refs.native.value = this.db[this.optionIndex].value
                this.elSelectNative = this.db[this.optionIndex].content
                this.closeSelectCustom()
            }

            if(this.Active && e.keyCode === 27){
                this.closeSelectCustom()
            }
        }
    },

    created() {
        document.addEventListener('click', this.closeSelectRoot)
        document.addEventListener('keydown', this.KeyboardNavigation)
    },
    destroy() {
        document.removeEventListener('click', this.closeSelectRoot)
        document.removeEventListener('keydown', this.KeyboardNavigation)
    }
}
</script>

<style lang="scss">

    .selectNative,
    .selectCustom {
    position: relative;
    width: 22rem;
    height: 4rem;
    }


    .selectCustom {
    position: absolute;
    top: 0;
    left: 0;
    display: none;
    }

    @media (hover: hover) {
        .selectCustom {
            display: block;
        }

        .selectNative:focus + .selectCustom {
            display: none;
        }
    }

    .selectNative:focus,
    .selectCustom.isActive .selectCustom-trigger {
    outline: none;
    box-shadow: white 0 0 0 0.2rem, #ff821f 0 0 0 0.4rem;
    }

    .select {
    position: relative;
    }

    .selectLabel {
    display: block;
    font-weight: bold;
    margin-bottom: 0.4rem;
    }

    .selectWrapper {
    position: relative;
    }

    .selectNative,
    .selectCustom-trigger {
    font-size: 1.6rem;
    background-color: #fff;
    border: 1px solid #6f6f6f;
    border-radius: 0.4rem;
    }

    .selectNative {
    -webkit-appearance: none;
    -moz-appearance: none;
    background-image: url("data:image/svg+xml;utf8,<svg fill='black' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/><path d='M0 0h24v24H0z' fill='none'/></svg>");
    background-repeat: no-repeat;
    background-position-x: 100%;
    background-position-y: 0.8rem;
    padding: 0rem 0.8rem;
    }

    .selectCustom-trigger {
    position: relative;
    width: 100%;
    height: 100%;
    background-color: #fff;
    padding: 0.8rem 0.8rem;
    cursor: pointer;
    }

    .selectCustom-trigger::after {
    content: "▾";
    position: absolute;
    top: 0;
    line-height: 3.8rem;
    right: 0.8rem;
    }

    .selectCustom-trigger:hover {
    border-color: #8c00ff;
    }

    .selectCustom-options {
    position: absolute;
    top: calc(3.8rem + 0.8rem);
    left: 0;
    width: 100%;
    border: 1px solid #6f6f6f;
    border-radius: 0.4rem;
    background-color: #fff;
    box-shadow: 0 0 4px #e9e1f8;
    z-index: 1;
    padding: 0.8rem 0;
    display: none;
    }

    .selectCustom.isActive .selectCustom-options {
    display: block;
    }

    .selectCustom-option {
    position: relative;
    padding: 0.8rem;
    padding-left: 2.5rem;
    }

    .selectCustom-option.isHover,
    .selectCustom-option:hover {
    background-color: #865bd7; // contrast AA
    color: white;
    cursor: default;
    }

    .selectCustom-option:not(:last-of-type)::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    border-bottom: 1px solid #d3d3d3;
    }

    .selectCustom-option.isActive::before {
    content: "✓";
    position: absolute;
    left: 0.8rem;
    }

    // ----- Theme styles -----

    html {
    font-size: 62.5%;
    }
    body {
    background: #f8f3ef;
    font-family: Arial, Helvetica, sans-serif;
    box-sizing: border-box;
    color: #343434;
    line-height: 1.5;
    font-size: 1.6rem;
    min-height: 120vh; /* using arrow keys in the select, does not scroll the page */
    }

    body * {
    box-sizing: inherit;
    }

    strong {
    font-weight: 600;
    }

    .title {
    font-size: 2rem;
    font-weight: 600;
    margin: 1.6rem;
    line-height: 1.2;
    text-align: center;
    }

    .card {
    position: relative;
    margin: 2rem auto;
    max-width: calc(100% - 2rem);
    width: 40rem;
    background: white;
    padding: 3rem;
    box-shadow: 0.2rem 0.2rem #e9e1f8;
    }

    .inst {
    margin-bottom: 1rem;
    }

    .note {
    font-size: 1.4rem;
    margin: 2rem 0 0;
    color: #6b6b6b;
    }

    .link {
        display: inline-block;
        color: inherit;
        text-decoration-color: #9b78de;
        padding: 0.1rem 0.2rem;
        transform: translateX(-0.1em);
        margin-right: -0.1em;

        &:hover {
            color: #8c00ff;
        }

        &:focus {
            outline: none;
            background-color: #e9e1f8;
        }
    }
</style>