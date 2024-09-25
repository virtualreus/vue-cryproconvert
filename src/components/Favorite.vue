<template>
    <h2>Избранное: </h2>
    <div v-for="(el, index) in favs" :key="index" @click="getFromFavs(index)">
        <span>{{ el.from }}</span>
        <span>{{ el.to }}</span>
    </div>
</template>

<script>
export default {
    props: {
        favs: {
            type: Array,
            required: true
        },
        getFromFavs: {
            type: Function,
            required: true
        }
    }
}
</script>

<style scoped>
h2 {
    margin-top: 20px;
    color: white;
}

div {
    display: flex;
    justify-content: space-between;
    width: 500px;
    margin: 10px auto;
    transition: all 500ms ease;
}

span {
    padding: 10px 15px;
    background-color: #8c00ff;
    cursor: pointer;
    color: white;
}
div:hover {
    opacity: 0.7;
    transform: scale(1.1);
    cursor: pointer;
}
</style>