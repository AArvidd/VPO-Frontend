<script setup>
let entry = defineProps({
    in: Object,

    // name: {
    //     type: String,
    //     Required: true
    // },
    // description: String,
    // faction: {
    //     type: String,
    //     Required: true
    // },
    // points: {
    //     type: Number,
    //     Request: true
    // },
    // tags: [String]
});


</script>


<template>
    <div id="root">
        <h2>{{ entry.in.name }}</h2>
        <div id="midel">
            <p>Faction: {{ entry.in.faction }}</p>
            <p>Points: {{ entry.in.points }}</p>
        </div>
        <div v-if="entry.in.description">
            <p>Description</p>
            <p>{{ entry.in.description }}</p>
        </div>
    </div>
</template>


<style scoped>

#root {
    height: 200px;
    overflow: hidden;
}

#midel {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}

</style>