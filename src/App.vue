<template>
<div>
    <p><label><input type="radio" value="one" v-model="arr">1</label></p>	
    <p><label><input type="radio" value="two" v-model="arr">2</label></p>	
    <p>{{arr}}</p>

    <select v-model='selected'>
        <option  
            v-for="option in options" 
            :key="option.value"
            :value='option.value'
        >
            {{option.text}}
        </option>
    </select>
    <p>{{selected}}</p>
    <p><label><input type="radio" name='of' v-model='select' :value='a'></label></p>
    <p><label><input type="radio" name='of' v-model='select' :value='a'></label></p>
    <!-- <p><label><input  v-model.lazy='select'></label></p> -->
    <p><label><input type='number'  v-model="select"></label></p>
    <p>{{select}}</p>
    <baseButton></baseButton>
</div>
</template>

<script>
import baseButton from './components/baseButton.vue'
export default {
  components: { baseButton },
    data() {
        return {
            name: 'App',
            select: 0,
            a: true,
            selected: 'A',
             options: [
                { text: 'Один', value: 'A' },
                { text: 'Два', value: 'B' },
                { text: 'Три', value: 'C' }
            ]
        }
    }
}
</script>

<style>
    :root {
    --number-9: 0.25;
    --number-8: 0.16;
    --number-7: 0.08;
    --number-6: 0.0001;

    --blue50: #EBF4F8;
    --blue100: #DBE2EA;
    --blue600: #0880AE;
    --blue900: #2C2738;

    --black9: rgba(0, 0, 0, var(--number-9));
    --black8: rgba(44, 39, 56, var(--number-7));
    --black7: rgba(44, 39, 56, var(--number-8));
    --black6: rgba(44, 39, 56, var(--number-6));

    --dropShadow: drop-shadow(0px 4px 4px var(--black9));
    --textShadow: 0px 4px 4px var(--black9);
    --shadowNormal: 
        0px 2px 4px var(--black7), 
        0px 4px 8px var(--black7);
    --shadowHover: 
        0px 12px 24px var(--black7),
        0px 24px 48px var(--black8);
    --shadowActive: 
        0px 2px 4px var(--black6), 
        0px 4px 8px var(--black7);
        
    }
    @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@500&display=swap');
</style>


