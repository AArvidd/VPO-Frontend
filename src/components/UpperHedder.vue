<script setup>
    import { computed, ref, watch } from "vue"
    let emit = defineEmits(['uppdate', "chainge"]);

    let SearchOptions = [] // from database
    let searchInput = ref("");
    let searchFocus = ref(false);
    let hover = ref(false);

    getSeartchOptions()
    
    
    let filterdList = computed(() => {
        return SearchOptions.filter((t) => t.toLocaleLowerCase().includes(searchInput.value.toLocaleLowerCase()));
    })
    
    function click(s){
        searchInput.value = s;
        emit("chainge", 1);
    }
    
    
    watch(searchInput, () => {emit('uppdate', searchInput.value)})
    
    async function getSeartchOptions(){
        let respons = await fetch("http://localhost:3030/factions")
        let factions = await respons.json()
        
        for(let i in factions){
            SearchOptions.push(factions[i].name)
        }

        for(let i in factions){
            for(let tag in factions[i].tags){
                if(!SearchOptions.includes(factions[i].tags[tag])){
                    SearchOptions.push(factions[i].tags[tag]);
                }
            }
        }
    }

</script>

<template>
    <header>
        <div id="left" class="aria">
            <h1 @click="$emit('chainge', 0)">Hammer Finder</h1>
        </div>
        <div id="center" class="aria">
            <ul>
                <li @click="$emit('chainge', 2)">Poste challenge</li>
                <li @click="$emit('chainge', 1)">Find opponent</li>
            </ul>
        </div>
        <div id="right" class="aria">
            <input v-model="searchInput" @focus="searchFocus = true" @blur="searchFocus = false"  placeholder="search">
            <button @click="$emit('chainge', 1)">search</button>
            <div v-if="(searchFocus && searchInput !== '') || hover" id="options" @mouseover="hover = true" @mouseleave="hover = false">
                <ul>
                    <li class="option" v-for="element in filterdList.slice(0, 10)">
                        <p @click="click(element)">{{ element }}</p>
                    </li>
                </ul>
            </div>
        </div>
    </header>
</template>

<style scoped>

header {
    background-color: lightgray;
    width: 100%;
    margin: 0px;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
    border-bottom: 2px solid black;
}

.aria {
    margin: 10px;
}

#left {
    margin-left: 30px;
}

#right {
    margin-right: 30px;
    height: 25px;
    /* overflow: hidden; */
}

#center > ul {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 300px;
}

#options {
    background-color: white;
    border: 2px solid black;
    border-radius: 10px;
}

.option:hover {
    background-color: lightgray;
}

a {
    color: black;
}

</style>