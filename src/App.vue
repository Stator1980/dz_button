<script setup>
// import Button from "./components/Button.vue";
import { onBeforeMount, ref } from "vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";

const API_ENDPOINT = "http://localhost:8080/api/random-words";

let data = ref();

let rate = ref({
    rating: "99",
});

async function getCards() {
    const res = await fetch(`${API_ENDPOINT}`);
    data.value = await res.json();
    data._rawValue.newKey = "countCard";
    data._rawValue.newKey = "state";
    data._rawValue.newKey = "status";

    for (let i = 0; i < 10; i++) {
        data._rawValue[i].state = "closed";
        data._rawValue[i].status = "pending";
        if (i < 9) {
            data._rawValue[i].countCard = "0" + (i + 1);
        } else {
            data._rawValue[i].countCard = "10";
        }
    }
    console.log(data._rawValue);
}

onBeforeMount(() => {
    getCards();
});

function getRotate() {
    console.log("ROTATE");
}

function getTranslateWrong() {
    console.log("TranslateWrong");
}

function getTranslateSuccess() {
    console.log("TranslateSuccess");
}
</script>

<template>
    <div class="content">
        <Score v-bind="rate" />
        <!-- <Button>Начать игру </Button> -->
        <div class="card-row">
            <Card
                v-for="item in data"
                v-bind="item"
                :key="item.word"
                @card-rotate="getRotate"
                @card-wrong="getTranslateWrong"
                @csardSuccess="getTranslateSuccess"
            />
        </div>
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
}
</style>
