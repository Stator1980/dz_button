<script setup>
import IconHeart from "../icons/IconHeart.vue";
import Button from "./Button.vue";

const { rating = 0 } = defineProps({
    rating: Number,
});
</script>

<template>
    <div class="header">
        <div class="name-game">Запомни слово</div>
        <Button class="count-like">
            {{ rating }}
            <IconHeart />
        </Button>
    </div>
</template>

<style scoped>
.header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    min-width: 1200px;
}

.name-game {
    /* position: absolute; */
    width: 161px;
    height: 24px;
    top: 49px;
    left: 66px;
    font-family: var(--font);
    font-weight: 700;
    font-size: 16px;
    letter-spacing: 0.12em;
    line-height: 24px;
    color: var(--color-header);
    text-transform: uppercase;
}

.count-like {
    width: 110px;
    height: 48px;
    border-radius: 36px;
    padding-top: 12px;
    padding-right: 24px;
    padding-bottom: 12px;
    padding-left: 24px;
    background: #cce8ff;
    font-family: Roboto;
    font-weight: 700;
    font-size: 16px;
    line-height: 24px;
    text-align: center;
    color: #008bfe;
    display: flex;
    align-items: center;
}
</style>
