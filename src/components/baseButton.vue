<template>
    <button><slot>Button</slot></button>
</template>

<style lang="scss">

button {
    appearance: none;
    border: 0;
    border-radius: 0;
    background: none;
    color: inherit;
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
    color: var(--blue900);
    font-family: 'IBM Plex Sans', sans-serif;
    background-color: var(--cyan-blue200);
    border: 2px solid var(--blue200);
    
    &:hover {
        box-shadow: var(--shadowHover);    
    }

    &:active {
        box-shadow: var(--shadowActive);    
    }
    
    &:disabled {
        background-color: var(--grey100);
        color: var(--red800);
        opacity: 0.5;
        box-shadow: none;    
        text-shadow: none;
    }
}
</style>