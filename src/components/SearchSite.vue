<script setup>
import { compile, computed, watch, inject } from "vue";
import sArticle from "./SearchArticle.vue";

let inputs = defineProps({
    search: String,
})

let list = [    // from database
    {
        name: "Army one",
        description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, soluta, perferendis delectus tempore voluptates quam ratione quis a illo asperiores quae animi pariatur repudiandae amet aliquid et in consequatur. Nisi?",
        faction: "Necron",
        points: 2000
    },
    {
        name: "My army",
        faction: "Ultramarines",
        points: 2000,
        tags: ["Space Marines"],
    },
    {
        name: "theft",
        faction: "Blodraven",
        points: 2000,
        tags: ["Space Marinse"]
    },
    {
        name: "WAAAAAH",
        description: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Veniam, soluta, perferendis delectus tempore voluptates quam ratione quis a illo asperiores quae animi pariatur repudiandae amet aliquid et in consequatur. Nisi?",
        faction: "Orks",
        points: 3000,
        tags: ["gork", "mork"],
    },
]

let factions = [ // from database
    "Ultramarines",
    "Necron",
    "Orks"
]

let filterdList = computed(() => {
    return list.filter((t) => {
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