<template>
    <DocSectionText v-bind="$attrs">
        <p>Image is used similar to the standard <i>img</i> element.</p>
    </DocSectionText>
    <div class="card flex justify-content-center">
        <Image src="https://primefaces.org/cdn/primevue/images/galleria/galleria7.jpg" alt="Image" width="250" />
    </div>
    <DocSectionCode :code="code" />
</template>

<script>
export default {
    data() {
        return {
            code: {
                basic: `
<Image src="https://primefaces.org/cdn/primevue/images/galleria/galleria7.jpg" alt="Image" width="250" />
`,
                options: `
<template>
    <div class="card flex justify-content-center">
        <Image src="https://primefaces.org/cdn/primevue/images/galleria/galleria7.jpg" alt="Image" width="250" />
    </div>
</template>
`,
                composition: `
<template>
    <div class="card flex justify-content-center">
        <Image src="https://primefaces.org/cdn/primevue/images/galleria/galleria7.jpg" alt="Image" width="250" />
    </div>
</template>`
            }
        };
    }
};
</script>
