<template>
    <DocSectionText v-bind="$attrs">
        <p>Main configuration settings of PrimeVue, refer to the <PrimeVueNuxtLink to="/configuration">configuration</PrimeVueNuxtLink> documentation for details. Defaults to an empty object.</p>
    </DocSectionText>
    <DocSectionCode :code="code" importCode hideToggleCode hideCodeSandbox hideStackBlitz />
</template>

<script>
export default {
    data() {
        return {
            code: {
                basic: `
primevue: { 
    options: {
        unstyled: true,
        ripple: true,
        inputStyle: 'filled',
        pt: {

        }
    }
}
`
            }
        };
    }
};
</script>
