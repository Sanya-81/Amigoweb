<template>
<div>
    <button>Button</button>
    <button class="button">Button</button>
</div>
</template>

<style lang="scss" scoped>
    
    button {
        appearance: none;
        border: 0;
        border-radius: 0;
        background: #fff;
    }

    .button {
        display: flex;
        justify-content: center;
        align-items: center;
        
        width:  180px;
        height: 56px;
        border-radius: 6px;

        color: var(--blue50);
        font-family: 'IBM Plex Sans', sans-serif;
        box-shadow: var(--shadowNormal);
        text-shadow: var(--textShadow);
        background-color: var(--blue600);
        
        &:hover {
            text-shadow: none;
            box-shadow: var(--shadowHover);    
            filter: var(--dropShadow)
        }

        &:active {
            border: 2px solid var(--blue900);
            box-shadow: var(--shadowActive);    
        }
    }
</style>