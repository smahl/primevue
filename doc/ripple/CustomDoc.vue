<template>
    <DocSectionText v-bind="$attrs">
        <p>Default styling of the animation adds a shade of white. This can easily be customized using css that changes the color of <i>p-ink</i> element.</p>
    </DocSectionText>
    <div class="card flex justify-content-center align-items-center gap-2">
        <div v-ripple class="p-ripple box styled-box-green shadow-2">Green</div>
        <div v-ripple class="p-ripple box styled-box-orange shadow-2">Orange</div>
        <div v-ripple class="p-ripple box styled-box-purple shadow-2">Purple</div>
    </div>
    <DocSectionCode :code="code" />
</template>

<script>
export default {
    data() {
        return {
            code: {
                basic: `
<div v-ripple class="p-ripple box styled-box-green shadow-2">Green</div>
<div v-ripple class="p-ripple box styled-box-orange shadow-2">Orange</div>
<div v-ripple class="p-ripple box styled-box-purple shadow-2">Purple</div>
`,
                options: `
<template>
    <div class="flex justify-content-center align-items-center">
        <div v-ripple class="p-ripple box styled-box-green shadow-2">Green</div>
        <div v-ripple class="p-ripple box styled-box-orange shadow-2">Orange</div>
        <div v-ripple class="p-ripple box styled-box-purple shadow-2">Purple</div>
    </div>
</template>

<style scoped>
::v-deep(.styled-box-green .p-ink) {
    background: rgba(75, 175, 80, 0.3);
}
::v-deep(.styled-box-orange .p-ink) {
    background: rgba(255, 193, 6, 0.3);
}

::v-deep(.styled-box-purple .p-ink) {
    background: rgba(156, 39, 176, 0.3);
}

.box {
    background: var(--surface-card);
    padding: 2rem;
    border-radius: 10px;
    width: 110px;
    text-align: center;
}
</style>
`,
                composition: `
<template>
    <div class="flex justify-content-center align-items-center">
        <div v-ripple class="p-ripple box styled-box-green shadow-2">Green</div>
        <div v-ripple class="p-ripple box styled-box-orange shadow-2">Orange</div>
        <div v-ripple class="p-ripple box styled-box-purple shadow-2">Purple</div>
    </div>
</template>

<style scoped>
::v-deep(.styled-box-green .p-ink) {
    background: rgba(75, 175, 80, 0.3);
}
::v-deep(.styled-box-orange .p-ink) {
    background: rgba(255, 193, 6, 0.3);
}

::v-deep(.styled-box-purple .p-ink) {
    background: rgba(156, 39, 176, 0.3);
}

.box {
    background: var(--surface-card);
    padding: 2rem;
    border-radius: 10px;
    width: 110px;
    text-align: center;
}
</style>`
            }
        };
    }
};
</script>

<style scoped>
.box {
    background: var(--surface-card);
    padding: 2rem;
    border-radius: 10px;
    width: 110px;
    text-align: center;
}

::v-deep(.styled-box-green .p-ink) {
    background: rgba(75, 175, 80, 0.3);
}
::v-deep(.styled-box-orange .p-ink) {
    background: rgba(255, 193, 6, 0.3);
}

::v-deep(.styled-box-purple .p-ink) {
    background: rgba(156, 39, 176, 0.3);
}
</style>
