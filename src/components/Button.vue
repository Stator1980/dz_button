<script setup>
const color_button = "button_green";
</script>

<template>
    <button :class ="color_button">
        <slot />
    </button>
</template>

<style scoped>
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

.button_red {
    border: none;
    border-radius: 100px;
    background: var(--color-bg-button-red);
    padding: 10px 16px;
    font-family: var(--font);
    font-size: 24px;
    font-weight: 400;
    color: var(--color-primary);
    cursor: pointer;
    width: 335px;
    height: 68px;
}

.button_green {
    border: none;
    border-radius: 100px;
    background: var(--color-bg-button-green);
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
