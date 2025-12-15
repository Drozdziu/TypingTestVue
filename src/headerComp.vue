<script setup lang="ts">
import { computed, ref, watch } from 'vue';

const darkTheme = ref(true);
const lang = ref(["Typing test", "Dark mode", "Light mode"]);

const emit = defineEmits<{changeLanguage: [lang: string]}>();

watch(darkTheme, (newValue) => {
    const root = document.documentElement;
    newValue ? root.removeAttribute('data-theme') : root.setAttribute('data-theme', 'light');
})
const changeLang = (l: string) => {
    emit('changeLanguage', l);
    switch (l) {
        case 'english':
            lang.value[0] = "Typing test";
            lang.value[1] = "Dark mode";
            lang.value[2] = "Light mode";
            break;
        case 'polish':
            lang.value[0] = "Test pisania";
            lang.value[1] = "Ciemny motyw";
            lang.value[2] = "Jasny motyw";
            break;
        case 'italian':
            lang.value[0] = "Prova di dattilografia";
            lang.value[1] = "Modalità oscura";
            lang.value[2] = "Modalità luce";
            break;
    }
}
</script>

<template>
    <header>
        <div>
            <h1>{{ lang[0] }}</h1>
        </div>
        <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" role="switch" id="flexSwitchCheckDefault"
                v-model="darkTheme" checked>
            <label class="form-check-label" for="flexSwitchCheckDefault">{{ darkTheme ? lang[1] : lang[2]   }}</label>
        </div>
        <div>
            <button @click="changeLang('english')"><i class="fi fi-gb" /></button>
            <button @click="changeLang('polish')"><i class="fi fi-pl" /></button>
            <button @click="changeLang('italian')"><i class="fi fi-it" /></button>
        </div>
    </header>
</template>
<style scoped>
div {
    padding: 10px;
}

label {
    font-size: 20px;
}

.form-check {
    display: block;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.form-check-input {
    float: right;
}

p {
    float: right;
}

button {
    border: 0;
    background-color: rgba(0, 0, 0, 0);    
}

</style>
