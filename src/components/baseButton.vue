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
        color: var(--blue50);
        background-color: var(--blue600);
        border-radius: 6px;
        box-shadow: var(--shadowNormal);
        font-family: 'IBM Plex Sans', sans-serif;
        text-shadow: var(--textShadow);
        
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