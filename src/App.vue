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
        <Card
            v-bind="cards[2]"
            @card-rotate="getRotate"
            @card-wrong="getTranslateWrong"
            @cardSuccess="getTranslateSuccess"
        />
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
</style>
