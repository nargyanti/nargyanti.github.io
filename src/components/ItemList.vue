<script setup>
import { computed } from "vue";
import { Icon } from "@iconify/vue";

const props = defineProps({
    list_title: {
        type: String,
    },
    items: {
        type: Array,
        required: true,
    },
    column: {
        type: [Number, String],
        default: 2,
    },
});

const gridColumn = computed(() => {
    const colMap = {
        1: "grid-cols-1",
        2: "grid-cols-2",
        3: "grid-cols-3",
        4: "grid-cols-4",
    };
    return colMap[props.column] || "grid-cols-2";
});
</script>

<template>
    <p v-if="list_title" class="my-1 text-gray-700">{{ list_title }}</p>
    <ul class="grid gap-x-5 gap-y-1" :class="gridColumn">
        <li v-for="(item, index) in items" :key="index" class="flex items-start py-1">
            <Icon icon="f7:bolt-fill" class="mr-2 mt-1 flex-shrink-0 text-primary" width="20" height="20" />
            <span class="flex-grow text-slate-700">{{ item }}</span>
        </li>
    </ul>
</template>
