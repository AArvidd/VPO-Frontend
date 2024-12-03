<script setup>
    import { computed, ref, watch } from "vue"

    let SearchOptions = ["40000", "40k", "Age of Sigmar", "AOS", "Space Marines", "Skaven"]; // from database

    let searchInput = ref("");

    let viseble = "hidden";

    let filterdList = computed(() => {
        return SearchOptions.filter((t) => t.toLocaleLowerCase().includes(searchInput.value.toLocaleLowerCase()));
    })

    function displaySerchOptions(){
        if(searchInput.value === ""){
            viseble = "hidden"
        }else{
            viseble = "visible";
        }
    }

    function search(){
        
    }

    watch(searchInput, displaySerchOptions)

</script>

<template>
    <header>
        <div id="left" class="aria">
            <h1>
                <a href="">Hammer Finder</a>
            </h1>
        </div>
        <div id="center" class="aria">
            <ul>
                <li><a href="">poste challenge</a></li>
                <li><a href="">find opponent</a></li>
            </ul>
        </div>
        <div id="right" class="aria">
            <input v-model="searchInput" placeholder="search">
            <button @click="search">search</button>
            <div :style="{visibility: viseble}" id="options">
                <ul>
                    <li class="option" v-for="element in filterdList">
                        <p>{{ element }}</p>
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