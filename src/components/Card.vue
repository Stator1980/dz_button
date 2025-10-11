<script setup>
import Label from "./Label.vue";
import Button from "./Button.vue";
import { ref } from "vue";
import IconClose from "../icons/IconClose.vue";
import IconCloseBig from "../icons/IconCloseBig.vue";
import IconTick from "../icons/IconTick.vue";
import IconSuccess from "../icons/IconSuccess.vue";

const {
    wordEng = "dust-coat",
    wordRus = "Верблюд",
    countCard = "01",
} = defineProps({
    wordEng: String,
    wordRus: String,
    countCard: String,
});

const isShow = ref(true);
const isShowBtClose = ref(false);
const isShowBtSuccess = ref(false);
const isShowLbFinish = ref(false);

const emit = defineEmits(["cardRotate", "cardWrong", "cardSuccess"]);

function rotate() {
    isShow.value = !isShow.value;
    //  console.log("1 - " + vShow);
    emit("cardRotate");
}

function translateWrong() {
    isShowLbFinish.value = ref(true);
    isShowBtClose.value = !isShowBtClose.value;
    emit("cardWrong");
}

function translateSuccess() {
    isShowLbFinish.value = ref(true);
    isShowBtSuccess.value = !isShowBtSuccess.value;
    emit("cardSuccess");
}
</script>

<template>
    <div class="cover">
        <div class="card">
            <div class="top-card">
                <Label>{{ countCard }}</Label>
                <IconCloseBig
                    :class="
                        (isShowBtClose && 'top-icon-close') ||
                        'card-rotate-hide'
                    "
                />
                <IconSuccess
                    :class="
                        (isShowBtSuccess && 'top-icon-close') ||
                        'card-rotate-hide'
                    "
                />
            </div>

            <Label class="middle-label">{{ isShow ? wordEng : wordRus }}</Label>
            <Label
                :class="
                    (isShowLbFinish && 'bottom-label') || 'card-rotate-hide'
                "
                >Завершено</Label
            >

            <div
                :class="(isShowLbFinish && 'card-rotate-hide') || 'bottom-card'"
            >
                <Button
                    :class="(isShow && 'card-rotate') || 'card-rotate-hide'"
                    @click="rotate()"
                    >Перевернуть</Button
                >
                <div class="bottom-bt">
                    <Button
                        :class="(isShow && 'card-rotate-hide') || 'card-close'"
                        @click="translateWrong()"
                    >
                        <IconClose />
                    </Button>
                    <Button
                        :class="(isShow && 'card-rotate-hide') || 'card-close'"
                        @click="translateSuccess()"
                    >
                        <IconTick />
                    </Button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.cover {
    width: 250px;
    height: 376px;
    border: none;
    border-radius: 15px;
    background: var(--color-primary);
}

.card {
    width: 212px;
    height: 320px;
    top: 28px;
    left: 19px;
    border-radius: 12px;
    border-width: 1px;
    border: 1px solid #cce8ff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-top: 28px;
    margin-left: 19px;
}

.middle-label {
    min-width: 180px;
    min-height: 21px;
    text-align: center;
    margin-left: 18px;
}

.card-rotate {
    max-width: 97px;
    max-height: 18px;
    margin-left: 57px;
    margin-bottom: -9px;
    font-family: var(--font);
    font-size: 12px;
    font-weight: 700;
    color: var(--color-header);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    background: var(--color-primary);
    padding: 0;
}

.card-rotate-hide {
    display: none;
}

.card-rotate:hover {
    background: var(--color-bg-button-green);
}

.card-close {
    max-width: 24px;
    max-height: 24px;
    color: var(--color-header);
    background: var(--color-primary);
    padding: 0;
}

.bottom-card {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
}

.bottom-bt {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-left: 70px;
    min-width: 75px;
    margin-bottom: -12px;
}

.top-card {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: -12px;
    margin-top: -20px;
    margin-left: 15px;
    max-width: 110px;
    min-height: 40px;
}

.top-icon-close {
    max-width: 48px;
    max-height: 48px;
    color: var(--color-header);
    background: var(--color-primary);
    padding: 0;
}

.bottom-label {
    max-width: 85px;
    max-height: 18px;
    margin-left: 60px;
    margin-bottom: -9px;
    font-family: var(--font);
    font-size: 12px;
    font-weight: 700;
    color: var(--color-header);
    letter-spacing: 0.12em;
    text-transform: uppercase;
}
</style>
