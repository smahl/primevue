<template>
    <DocSectionText v-bind="$attrs">
        <p>A column can be fixed during horizontal scrolling by enabling the <i>frozen</i> property on a Column. The location is defined with the <i>alignFrozen</i> that can be <i>left</i> or <i>right</i>.</p>
    </DocSectionText>
    <div class="card">
        <TreeTable :value="nodes" scrollable scrollHeight="200px" scrollDirection="both">
            <Column field="name" header="Name" expander frozen style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 2" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 2" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 3" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 3" style="width: 250px; height: 57px"></Column>
        </TreeTable>
    </div>
    <DocSectionCode :code="code" :service="['NodeService']" />
</template>

<script>
import { NodeService } from '@/service/NodeService';

export default {
    data() {
        return {
            nodes: null,
            code: {
                basic: `
<TreeTable :value="nodes" scrollable scrollHeight="200px" scrollDirection="both">
    <Column field="name" header="Name" expander frozen style="width: 250px; height: 57px"></Column>
    <Column field="size" header="Size" style="width: 250px; height: 57px"></Column>
    <Column field="type" header="Type 2" style="width: 250px; height: 57px"></Column>
    <Column field="size" header="Size 2" style="width: 250px; height: 57px"></Column>
    <Column field="type" header="Type 3" style="width: 250px; height: 57px"></Column>
    <Column field="size" header="Size 3" style="width: 250px; height: 57px"></Column>
</TreeTable>
`,
                options: `
<template>
    <div class="card">
        <TreeTable :value="nodes" scrollable scrollHeight="200px" scrollDirection="both">
            <Column field="name" header="Name" expander frozen style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 2" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 2" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 3" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 3" style="width: 250px; height: 57px"></Column>
        </TreeTable>
    </div>
</template>

<script>
import { NodeService } from '@/service/NodeService';

export default {
    data() {
        return {
            nodes: null,
        }
    },
    mounted() {
        NodeService.getTreeTableNodes().then((data) => (this.nodes = data));
    }
}
<\/script>
`,
                composition: `
<template>
    <div class="card">
        <TreeTable :value="nodes" scrollable scrollHeight="200px" scrollDirection="both">
            <Column field="name" header="Name" expander frozen style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 2" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 2" style="width: 250px; height: 57px"></Column>
            <Column field="type" header="Type 3" style="width: 250px; height: 57px"></Column>
            <Column field="size" header="Size 3" style="width: 250px; height: 57px"></Column>
        </TreeTable>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { NodeService } from '@/service/NodeService';

onMounted(() => {
    NodeService.getTreeTableNodes().then((data) => (nodes.value = data));
});

const nodes = ref();
<\/script>
`,
                data: `
{
    key: '0',
    label: 'Documents',
    data: 'Documents Folder',
    icon: 'pi pi-fw pi-inbox',
    children: [
        {
            key: '0-0',
            label: 'Work',
            data: 'Work Folder',
            icon: 'pi pi-fw pi-cog',
            children: [
                { key: '0-0-0', label: 'Expenses.doc', icon: 'pi pi-fw pi-file', data: 'Expenses Document' },
                { key: '0-0-1', label: 'Resume.doc', icon: 'pi pi-fw pi-file', data: 'Resume Document' }
            ]
        },
        {
            key: '0-1',
            label: 'Home',
            data: 'Home Folder',
            icon: 'pi pi-fw pi-home',
            children: [{ key: '0-1-0', label: 'Invoices.txt', icon: 'pi pi-fw pi-file', data: 'Invoices for this month' }]
        }
    ]
},
...
`
            }
        };
    },
    mounted() {
        NodeService.getTreeTableNodes().then((data) => (this.nodes = data));
    }
};
</script>
