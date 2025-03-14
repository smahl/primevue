<template>
    <DocSectionText v-bind="$attrs">
        <p>Thumbnails represent a smaller version of the actual content.</p>
    </DocSectionText>
    <div class="card">
        <div class="flex flex-wrap gap-3 mb-5 align-self-center">
            <div class="flex flex-wrap gap-3 mb-5">
                <div v-for="option in positionOptions" :key="option.label" class="flex align-items-center">
                    <RadioButton v-model="position" :inputId="option.label" name="option" :value="option.value" />
                    <label :for="option.label" class="ml-2"> {{ option.label }} </label>
                </div>
            </div>
        </div>
        <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="4" :thumbnailsPosition="position" containerStyle="max-width: 640px">
            <template #item="slotProps">
                <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
            </template>
            <template #thumbnail="slotProps">
                <div class="grid grid-nogutter justify-content-center">
                    <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
                </div>
            </template>
        </Galleria>
    </div>
    <DocSectionCode :code="code" :service="['PhotoService']" />
</template>

<script>
import { PhotoService } from '@/service/PhotoService';

export default {
    data() {
        return {
            images: null,
            position: 'bottom',
            positionOptions: [
                {
                    label: 'Bottom',
                    value: 'bottom'
                },
                {
                    label: 'Top',
                    value: 'top'
                },
                {
                    label: 'Left',
                    value: 'left'
                },
                {
                    label: 'Right',
                    value: 'right'
                }
            ],
            responsiveOptions: [
                {
                    breakpoint: '991px',
                    numVisible: 4
                },
                {
                    breakpoint: '767px',
                    numVisible: 3
                },
                {
                    breakpoint: '575px',
                    numVisible: 1
                }
            ],
            code: {
                basic: `
<Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="4" :thumbnailsPosition="position" containerStyle="max-width: 640px">
    <template #item="slotProps">
        <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
    </template>
    <template #thumbnail="slotProps">
        <div class="grid grid-nogutter justify-content-center">
            <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block;" />
        </div>
    </template>
</Galleria>
`,
                options: `
<template>
    <div class="card">
        <div class="flex flex-wrap gap-3 mb-5 align-self-center">
            <div class="flex flex-wrap gap-3 mb-5">
                <div v-for="option in positionOptions" :key="option.label" class="flex align-items-center">
                    <RadioButton v-model="position" :inputId="option.label" name="option" :value="option.value" />
                    <label :for="option.label" class="ml-2"> {{ option.label }} </label>
                </div>
            </div>
        </div>
        <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="4" :thumbnailsPosition="position" containerStyle="max-width: 640px">
            <template #item="slotProps">
                <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
            </template>
            <template #thumbnail="slotProps">
                <div class="grid grid-nogutter justify-content-center">
                    <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block;" />
                </div>
            </template>
        </Galleria>
    </div>
</template>

<script>
import { PhotoService } from '@/service/PhotoService';

export default {
    data() {
        return {
            images: null,
            position: 'bottom',
            positionOptions: [
                {
                    label: 'Bottom',
                    value: 'bottom'
                },
                {
                    label: 'Top',
                    value: 'top'
                },
                {
                    label: 'Left',
                    value: 'left'
                },
                {
                    label: 'Right',
                    value: 'right'
                }
            ],
            responsiveOptions: [
                {
                    breakpoint: '991px',
                    numVisible: 4
                },
                {
                    breakpoint: '767px',
                    numVisible: 3
                },
                {
                    breakpoint: '575px',
                    numVisible: 1
                }
            ]
        };
    },
    mounted() {
        PhotoService.getImages().then((data) => (this.images = data));
    }
};
<\/script>
`,
                composition: `
<template>
    <div class="card">
        <div class="flex flex-wrap gap-3 mb-5 align-self-center">
            <div class="flex flex-wrap gap-3 mb-5">
                <div v-for="option in positionOptions" :key="option.label" class="flex align-items-center">
                    <RadioButton v-model="position" :inputId="option.label" name="option" :value="option.value" />
                    <label :for="option.label" class="ml-2"> {{ option.label }} </label>
                </div>
            </div>
        </div>
        <Galleria :value="images" :responsiveOptions="responsiveOptions" :numVisible="4" :thumbnailsPosition="position" containerStyle="max-width: 640px">
            <template #item="slotProps">
                <img :src="slotProps.item.itemImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block" />
            </template>
            <template #thumbnail="slotProps">
                <div class="grid grid-nogutter justify-content-center">
                    <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="width: 100%; display: block;" />
                </div>
            </template>
        </Galleria>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { PhotoService } from '@/service/PhotoService';

const images = ref();
const position = ref('bottom');
const positionOptions = ref([
    {
        label: 'Bottom',
        value: 'bottom'
    },
    {
        label: 'Top',
        value: 'top'
    },
    {
        label: 'Left',
        value: 'left'
    },
    {
        label: 'Right',
        value: 'right'
    }
]);
const responsiveOptions = ref([
    {
        breakpoint: '991px',
        numVisible: 4
    },
    {
        breakpoint: '767px',
        numVisible: 3
    },
    {
        breakpoint: '575px',
        numVisible: 1
    }
]);

onMounted(() => {
    PhotoService.getImages().then((data) => (images.value = data));
});
<\/script>
`,
                data: `
/* PhotoService */
{
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria1.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria1s.jpg',
    alt: 'Description for Image 1',
    title: 'Title 1'
},
...
        `
            }
        };
    },
    mounted() {
        PhotoService.getImages().then((data) => (this.images = data));
    }
};
</script>
