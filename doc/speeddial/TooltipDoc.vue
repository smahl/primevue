<template>
    <DocSectionText v-bind="$attrs">
        <p>Items display a tooltip on hober when a standalone <PrimeVueNuxtLink to="/tooltip">Tooltip</PrimeVueNuxtLink> is present with a target that matches the items.</p>
    </DocSectionText>
    <div class="card">
        <div :style="{ position: 'relative', height: '350px' }">
            <SpeedDial :model="items" direction="up" class="right-0 bottom-0" buttonClass="p-button-help" :tooltipOptions="{ position: 'left' }" />
            <SpeedDial :model="items" direction="up" class="left-0 bottom-0" buttonClass="p-button-danger" :tooltipOptions="{ position: 'right' }" />
        </div>
    </div>
    <DocSectionCode :code="code" />
</template>

<script>
export default {
    data() {
        return {
            items: [
                {
                    label: 'Add',
                    icon: 'pi pi-pencil',
                    command: () => {
                        this.$toast.add({ severity: 'info', summary: 'Add', detail: 'Data Added' });
                    }
                },
                {
                    label: 'Update',
                    icon: 'pi pi-refresh',
                    command: () => {
                        this.$toast.add({ severity: 'success', summary: 'Update', detail: 'Data Updated' });
                    }
                },
                {
                    label: 'Delete',
                    icon: 'pi pi-trash',
                    command: () => {
                        this.$toast.add({ severity: 'error', summary: 'Delete', detail: 'Data Deleted' });
                    }
                },
                {
                    label: 'Upload',
                    icon: 'pi pi-upload',
                    command: () => {
                        this.$router.push('/fileupload');
                    }
                },
                {
                    label: 'Vue Website',
                    icon: 'pi pi-external-link',
                    command: () => {
                        window.location.href = 'https://vuejs.org/';
                    }
                }
            ],
            code: {
                basic: `
<SpeedDial :model="items" direction="up" class="right-0 bottom-0" buttonClass="p-button-help" :tooltipOptions="{ position: 'left' }" />
<SpeedDial :model="items" direction="up" class="left-0 bottom-0" buttonClass="p-button-danger" :tooltipOptions="{ position: 'right' }" />
`,
                options: `
<template>
    <div class="card">
        <div :style="{ position: 'relative', height: '350px' }">
            <SpeedDial :model="items" direction="up" class="right-0 bottom-0" buttonClass="p-button-help" :tooltipOptions="{ position: 'left' }" />
            <SpeedDial :model="items" direction="up" class="left-0 bottom-0" buttonClass="p-button-danger" :tooltipOptions="{ position: 'right' }" />
            <Toast />
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [
                {
                    label: 'Add',
                    icon: 'pi pi-pencil',
                    command: () => {
                        this.$toast.add({ severity: 'info', summary: 'Add', detail: 'Data Added' });
                    }
                },
                {
                    label: 'Update',
                    icon: 'pi pi-refresh',
                    command: () => {
                        this.$toast.add({ severity: 'success', summary: 'Update', detail: 'Data Updated' });
                    }
                },
                {
                    label: 'Delete',
                    icon: 'pi pi-trash',
                    command: () => {
                        this.$toast.add({ severity: 'error', summary: 'Delete', detail: 'Data Deleted' });
                    }
                },
                {
                    label: 'Upload',
                    icon: 'pi pi-upload',
                    command: () => {
                        this.$router.push('/fileupload');
                    }
                },
                {
                    label: 'Vue Website',
                    icon: 'pi pi-external-link',
                    command: () => {
                        window.location.href = 'https://vuejs.org/';
                    }
                }
            ]
        }
    }
};
<\/script>
`,
                composition: `
<template>
    <div class="card">
        <div :style="{ position: 'relative', height: '350px' }">
            <SpeedDial :model="items" direction="up" class="right-0 bottom-0" buttonClass="p-button-help" :tooltipOptions="{ position: 'left' }" />
            <SpeedDial :model="items" direction="up" class="left-0 bottom-0" buttonClass="p-button-danger" :tooltipOptions="{ position: 'right' }" />
            <Toast />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'primevue/usetoast';
import { useRouter } from 'vue-router';

const toast = useToast();
const router = useRouter();

const items = ref([
    {
        label: 'Add',
        icon: 'pi pi-pencil',
        command: () => {
            toast.add({ severity: 'info', summary: 'Add', detail: 'Data Added' });
        }
    },
    {
        label: 'Update',
        icon: 'pi pi-refresh',
        command: () => {
            toast.add({ severity: 'success', summary: 'Update', detail: 'Data Updated' });
        }
    },
    {
        label: 'Delete',
        icon: 'pi pi-trash',
        command: () => {
            toast.add({ severity: 'error', summary: 'Delete', detail: 'Data Deleted' });
        }
    },
    {
        label: 'Upload',
        icon: 'pi pi-upload',
        command: () => {
            router.push('/fileupload');
        }
    },
    {
        label: 'Vue Website',
        icon: 'pi pi-external-link',
        command: () => {
            window.location.href = 'https://vuejs.org/'
        }
    }
])
<\/script>
`
            }
        };
    }
};
</script>
