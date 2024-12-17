<script setup>
import { compile, computed, watch, inject, ref } from "vue";
import sArticle from "./SearchArticle.vue";

let inputs = defineProps({
    search: String,
})

let articles = ref([]) // from database
populate()

let filterdList = computed(() => {
    return articles.value.filter((t) => {
        if(inputs.search === ""){
            return true
        }
        if(t.faction.toLocaleLowerCase().includes(inputs.search.toLocaleLowerCase())){
            return true;
        }
        for(let i in t.tags){
            if(t.tags[i].toLocaleLowerCase().includes(inputs.search.toLocaleLowerCase())){
                return true;
            }
        }
        return false;
    })
})

async function populate(){
    let respons = await fetch("http://localhost:3030/article")
    articles.value = await respons.json()
}

</script>

<template>
    <div id="grid">
        <div class="block" v-for="entry in filterdList">
            <sArticle :in="entry" />
        </div>
        <div v-if="filterdList.length == 0" id="empty">
            <h1>No opponents are found</h1>
        </div>
    </div>
</template>

<style scoped>

#grid {
    margin: 30px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
}

#empty {
    height: 300px;
    text-align: center;
    align-content: center;
}

</style>