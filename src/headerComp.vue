<script lang="ts">
export default {
    name: 'headerComp',
}
</script>

<template>
    <header>
        <div>
            <h1>Typing Test</h1>
        </div>
        <div class="form-check form-switch">
            <input class="form-check-input" type="checkbox" role="switch" id="flexSwitchCheckDefault">
            <label class="form-check-label" for="flexSwitchCheckDefault">Dark mode</label>
        </div>
        <div>
            <button><i class="fi fi-gb" /></button>
            <button><i class="fi fi-pl" /></button>
            <button><i class="fi fi-it" /></button>
        </div>
    </header>
</template>

<style scoped>
div {
    padding: 10px;
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
label{
    color: #21FA91;
    font-size: large;
}

header {
    background-color: #222;
    width: 100%;
    min-width: 545px;
    padding: 10px;
    color: white;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    box-shadow: 0 0 5px #000;
}

button {
    background-color: rgba(0, 0, 0, 0);
    border: 0;
}

h1 {
    float: left;
    color: #21FA91;
}

i {
    width: 100px;
}
</style>
