<template>
<div class="f-prt__form-access access">
    <input name="check" id="check" type="checkbox" v-model="checked">
    <label for="check"><slot></slot></label>
</div>
</template>

<script>
export default {

}
</script>

<style>
 .f-prt__form-access {
        display: flex;
        align-items: center;
        gap: 10px;
        margin: 15px 0;
    }

</style>