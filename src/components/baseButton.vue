<template>
<div>
    <button>Button</button>
    <button disabled class="button"><slot>Button</slot></button>
    <button class="button"><slot>Button</slot></button>
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
        
        width: 80%;
        min-width: 180px;
        height: 56px;
        margin: 0 auto;
        border-radius: 6px;
        padding-left: 20px;
        padding-right: 20px;

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
        
        &:disabled {
            background-color: var(--blue100);
            color: var(--blue900);
            opacity: 0.5;
        }
    }
</style>