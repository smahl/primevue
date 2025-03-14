<template>
    <DocSectionText v-bind="$attrs">
        <p>Setting <i>orientation</i> to <i>horizontal</i> enables scrolling horizontally. In this case, the <i>itemSize</i> should refer to the width of an item.</p>
    </DocSectionText>
    <div class="card flex justify-content-center">
        <VirtualScroller :items="items" :itemSize="50" orientation="horizontal" class="border-1 surface-border border-round" style="width: 200px; height: 200px">
            <template v-slot:item="{ item, options }">
                <div :class="['flex align-items-center p-2', { 'surface-hover': options.odd }]" style="width: 50px; writing-mode: vertical-lr">{{ item }}</div>
            </template>
        </VirtualScroller>
    </div>
    <DocSectionCode :code="code" :dependencies="{ sass: '1.45.0', 'sass-loader': '8.0.2' }" />
</template>

<script>
export default {
    data() {
        return {
            items: null,
            code: {
                basic: `
<VirtualScroller :items="items" :itemSize="50" orientation="horizontal" class="border-1 surface-border border-round" style="width: 200px; height: 200px">
    <template v-slot:item="{ item, options }">
        <div :class="['flex align-items-center p-2', { 'surface-hover': options.odd }]" style="width: 50px; writing-mode: vertical-lr;">{{ item }}</div>
    </template>
</VirtualScroller>
`,
                options: `
<template>
    <div class="card flex justify-content-center">
        <VirtualScroller :items="items" :itemSize="50" orientation="horizontal" class="border-1 surface-border border-round" style="width: 200px; height: 200px">
            <template v-slot:item="{ item, options }">
                <div :class="['flex align-items-center p-2', { 'surface-hover': options.odd }]" style="width: 50px; writing-mode: vertical-lr;">{{ item }}</div>
            </template>
        </VirtualScroller>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: null
        };
    },
    created() {
        this.items = Array.from({ length: 100000 }).map((_, i) => \`Item #\${i}\`);
    }
};
<\/script>

<style lang="scss" scoped>
::v-deep(.p-virtualscroller) {
    .p-virtualscroller-content {
        display: flex;
        flex-direction: row;
    }
}
</style>
`,
                composition: `
<template>
    <div class="card flex justify-content-center">
        <VirtualScroller :items="items" :itemSize="50" orientation="horizontal" class="border-1 surface-border border-round" style="width: 200px; height: 200px">
            <template v-slot:item="{ item, options }">
                <div :class="['flex align-items-center p-2', { 'surface-hover': options.odd }]" style="width: 50px; writing-mode: vertical-lr;">{{ item }}</div>
            </template>
        </VirtualScroller>
    </div>
</template>

<script setup>
import { ref } from 'vue';

const items = ref(Array.from({ length: 100000 }).map((_, i) => \`Item #\${i}\`));
<\/script>

<style lang="scss" scoped>
::v-deep(.p-virtualscroller) {
    .p-virtualscroller-content {
        display: flex;
        flex-direction: row;
    }
}
</style>`
            }
        };
    },
    mounted() {
        this.items = Array.from({ length: 100000 }).map((_, i) => `Item #${i}`);
    }
};
</script>

<style lang="scss" scoped>
::v-deep(.p-virtualscroller) {
    .p-virtualscroller-content {
        display: flex;
        flex-direction: row;
    }
}
</style>
