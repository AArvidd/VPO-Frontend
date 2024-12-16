<script setup>

import { ref } from "vue"

let factions = [ // from database
    "Ultramarines",
    "Necron",
    "Orks"
]

let name = ref("");
let faction = ref("");
let points = ref();
let description = ref("");

function foo(form) {
    form.preventDefault();
    
}

</script>

<template>
    <article>
        <form v-on:submit="foo">
            <label for="name">Name </label>
            <input id="name" type="text" v-model="name" required> <br><br>
            
            <label for="faction">Faction </label> 
            <select id="faction" name="Faction" v-model="faction" required>
                <option v-for="faction in factions" :value="faction">{{ faction }}</option>
            </select> <br><br>
            
            <label for="points">Points </label> 
            <input id="points" type="number" v-model="points" required> <br><br>
            
            
            <label for="discription">description</label> <br>
            <textarea id="discription" name="description" v-model="description"></textarea> <br><br>
            
            <input type="submit">
        </form>
    </article>
</template>

<style scoped>

article {
    width: 500px;
    justify-self: center;
    margin-top: 70px;
}

textarea {
    resize: none;
    width: 400px;
    height: 150px;
}

</style>