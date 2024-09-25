<template>
    <input type="number" @input="changeAmount($event.target.value)" placeholder="Введите сумму: " min="0"><br>
    <button @click="convert()">Перевести</button>
    <button @click="favorite()">В избранное</button>
</template>

<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        },
        favorite: {
            type: Function,
            required: true
        }
    }
}
</script>

<style scoped>
input {
    border-radius: 3px;
    border: none;
    padding: 10px 15px;
    background-color: #fafafa;
    color: #333;
    outline: none; 
    width: 500px;
    font-size: 1.2em;
    position: relative;
    margin: 20px 0;
}

button {
    position: relative;
    padding: 15px 20px;
    color: white;
    text-transform: uppercase;
    cursor: pointer;
    background-color: #1a032d;
    border: 0;
    border-radius: 5px;
    transition: .2s;
    margin: 0 5px;
}

button:hover {
    transform: scale(1.1);
}
</style>
