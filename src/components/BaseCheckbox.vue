<template>
<div class="f-prt__form-checkbox">
    <input name="check" id="check" type="checkbox">
    <label for="check"><slot></slot></label>
</div>
</template>

<script>
export default {
   
}

</script>

<style>
 .f-prt__form-checkbox {
        display: flex;
        align-items: center;
        gap: 10px;
        margin: 15px 0;
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
        transform-origin: center;
        background: var(--green-cyan700);
        /* transform-origin: bottom left; */
        /* box-shadow: inset 2px 2px var(--cyan600); */
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
</style>