<script setup></script>

<template>
    <div class="label">
        <slot />
    </div>
</template>

<style scoped>
.label {
    width: 16px;
    height: 16px;
    top: 20px;
    left: 35px;
    background: var(--color-primary);
    font-family: var(--font);
    font-size: 14px;
    font-weight: 400;
    color: var(--color-black);
}
</style>
