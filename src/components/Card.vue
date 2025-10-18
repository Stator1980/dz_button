<script setup>
import Label from "./Label.vue";
import Button from "./Button.vue";
import { ref } from "vue";
import IconClose from "../icons/IconClose.vue";
import IconCloseBig from "../icons/IconCloseBig.vue";
import IconTick from "../icons/IconTick.vue";
import IconSuccess from "../icons/IconSuccess.vue";

const {
    word = "dust-coat",
    translation = "Караван верблюдов",
    countCard = "01",
} = defineProps({
    word: String,
    translation: String,
    countCard: String,
});

const sprState = {
    CLOSED: "closed ",
    OPENED: "opened",
};

const sprStatus = {
    SUCCESS: "success",
    FAIL: "fail",
    PENDING: "pending",
};

const state = ref(sprState.OPENED);
const status = ref(sprStatus.PENDING);

const emit = defineEmits(["cardRotate", "cardWrong", "cardSuccess"]);

function rotate() {
    if (state.value == sprState.OPENED) {
        state.value = sprState.CLOSED;
    } else state.value = sprState.OPENED;

    emit("cardRotate");
}

function translateWrong() {
    status.value = sprStatus.FAIL;
    emit("cardWrong");
}

function translateSuccess() {
    status.value = sprStatus.SUCCESS;
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
                        (status === sprStatus.FAIL && 'top-icon-close') ||
                        'card-rotate-hide'
                    "
                />
                <IconSuccess
                    :class="
                        (status === sprStatus.SUCCESS && 'top-icon-close') ||
                        'card-rotate-hide'
                    "
                />
            </div>

            <Label class="middle-label">{{
                state === sprState.OPENED ? word : translation
            }}</Label>
            <Label
                :class="
                    (status != sprStatus.PENDING && 'bottom-label') ||
                    'card-rotate-hide'
                "
                >Завершено</Label
            >

            <div
                :class="
                    (status != sprStatus.PENDING && 'card-rotate-hide') ||
                    'bottom-card'
                "
            >
                <Button
                    :class="
                        (state === sprState.OPENED && 'card-rotate') ||
                        'card-rotate-hide'
                    "
                    @click="rotate()"
                    >Перевернуть</Button
                >
                <div class="bottom-bt">
                    <Button
                        :class="
                            (state === sprState.OPENED && 'card-rotate-hide') ||
                            'card-close'
                        "
                        @click="translateWrong()"
                    >
                        <IconClose />
                    </Button>
                    <Button
                        :class="
                            (state === sprState.OPENED && 'card-rotate-hide') ||
                            'card-close'
                        "
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
