<script setup lang="ts">
import { ref, watch } from 'vue';

const darkTheme = ref(true);
watch(darkTheme, (newValue)=>{
    const root = document.documentElement;
    newValue ?  root.removeAttribute('data-theme')  : root.setAttribute('data-theme', 'light');
})
</script>

<template>
    <header>
        <div>
            <h1>Typing Test</h1>
        </div>
        <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" role="switch" id="flexSwitchCheckDefault" v-model="darkTheme" checked>
            <label class="form-check-label" for="flexSwitchCheckDefault">{{darkTheme ? "Dark Mode" : "Light Mode" }}</label>
        </div>
        <div>
            <button @click="$emit('changeLanguage', 'english');"><i class="fi fi-gb" /></button>
            <button @click="$emit('changeLanguage', 'polish');"><i class="fi fi-pl" /></button>
            <button @click="$emit('changeLanguage', 'italian');"><i class="fi fi-it" /></button>
        </div>
    </header>
</template>

<style scoped>
div {
    padding: 10px;
}
label{
    font-size: 20px;
}
.form-check {
    display: block;
}

.form-check-input {
    float: right;
}
p {
    float: right;
}
button {
    background-color: rgba(0, 0, 0, 0);
    border: 0;
}


</style>
