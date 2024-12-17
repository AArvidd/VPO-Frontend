<script setup>
    import { ref, onBeforeMount } from "vue"

    let emit = defineEmits("chainge")

    let factionTags
    
    let factions = ref([]); // from database
    
    
    getFactions();
    
    let name = ref("");
    let faction = ref("");
    let points = ref();
    let description = ref("");
    
    async function foo(form) {
        form.preventDefault();
        let out = {
            name: name.value,
            faction: faction.value,
            points: points.value,
            tags:[]
        }
        if(description.value){
            out["description"] = description.value
        }

        for(let i in factionTags){
            if(out.faction == factionTags[i].name){
                for(let j = 0; j < factionTags[j].tags.length; j++){
                    out.tags.push(factionTags[i].tags[j])
                }
                break;
            }
        }

        let jsonS = JSON.stringify(out)

        let respons = await fetch("http://localhost:3030/article", {method: "POST", body: jsonS})

        if(!respons.ok){
            alert("Bad request\nCould not send in challenge")
        }else{
            emit("chainge", 0)
        }
    }
    
    async function getFactions(){
        let respons = await fetch("http://localhost:3030/factions")
        factionTags = await respons.json()

        for(let i in factionTags){
            factions.value.push(factionTags[i].name)
        }
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