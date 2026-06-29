<script setup>
import { Icon } from "@iconify/vue";

defineProps({
    icon: {
        type: String,
        required: true,
    },
    size: {
        type: [Number, String],
        default: 22,
    },
    color: {
        type: String,
        default: "text-primary",
    },
    backgroundColor: {
        type: String,
        default: "bg-primary-content",
    },
    backgroundSize: {
        type: String,
        default: "p-2",
    },
});
</script>

<template>
    <div class="flex items-start">
        <div :class="['rounded-full', backgroundColor, backgroundSize]">
            <Icon :icon="icon" :width="size" :height="size" :class="color" />
        </div>
    </div>
</template>
