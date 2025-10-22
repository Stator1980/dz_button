<script setup>
// import Button from "./components/Button.vue";
import { ref } from "vue";
import Card from "./components/Card.vue";
import Score from "./components/Score.vue";

let rate = ref({
    rating: "99",
});

const cards = ref([
    {
        word: "dust-coat",
        translation: "Караван верблюдов",
        state: "closed",
        status: "pending",
    },
    {
        word: "carom",
        translation: "свинец",
        state: "closed",
        status: "pending",
    },
    {
        word: "car",
        translation: "Автомобиль",
        state: "closed",
        status: "pending",
    },
    {
        word: "vino",
        translation: "Вино",
        state: "closed",
        status: "pending",
    },
]);

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
                v-for="item in cards"
                v-bind="item"
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
    gap: 20px;
}
</style>
