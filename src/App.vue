<script setup>
import Button from "./components/Button.vue";
import { onBeforeMount, ref } from "vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";

const API_ENDPOINT = "http://localhost:8080/api/random-words";

let data = ref();

let rate = ref({
    rating: 0,
});

let isStart = ref(false);

async function getCards() {
    const res = await fetch(`${API_ENDPOINT}`);
    data.value = await res.json();
    data.value.newKey = "countCard";
    data.value.newKey = "state";
    data.value.newKey = "status";

    for (let i = 0; i < 10; i++) {
        data.value[i].state = "closed";
        data.value[i].status = "pending";
        if (i < 9) {
            data.value[i].countCard = "0" + (i + 1);
        } else {
            data.value[i].countCard = "10";
        }
    }
    //console.log(data.value);
}

onBeforeMount(() => {
    getCards();
});

function getRotate() {
    console.log("ROTATE");
}

function getTranslateWrong() {
    rate.value.rating = rate.value.rating - 4;
}

function getTranslateSuccess() {
    rate.value.rating = rate.value.rating + 10;
}

function startGame() {
    isStart.value = true;
}

function startAgain() {
    rate.value.rating = 0;
    getCards();
}
</script>

<template>
    <div class="content">
        <Score v-bind="rate" />
        <Button v-if="!isStart" @click="startGame()" class="button_blue"
            >Начать игру
        </Button>
        <div v-if="isStart" class="card-row">
            <Card
                v-for="item in data"
                v-bind="item"
                :key="item.word"
                @card-rotate="getRotate"
                @card-wrong="getTranslateWrong"
                @card-success="getTranslateSuccess"
            />
        </div>
        <Button v-if="isStart" @click="startAgain()" class="button_blue"
            >Начать занова
        </Button>
    </div>
</template>

<style scoped>
.content {
    display: grid;
    gap: 20px;
    min-height: 800px;
    grid-template-rows: 200px auto;
    justify-content: center;
    place-items: center;
}

.card-row {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    margin-bottom: 80px;
}

.button_blue {
    border: none;
    border-radius: 100px;
    background: var(--color-bg-button-blue);
    padding: 10px 16px;
    font-family: var(--font);
    font-size: 24px;
    font-weight: 400;
    color: var(--color-primary);
    cursor: pointer;
    width: 335px;
    height: 68px;
}
</style>
