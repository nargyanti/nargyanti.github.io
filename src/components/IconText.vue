<script setup>
import { computed } from "vue";
import { Icon } from "@iconify/vue";

const props = defineProps({
    icon: {
        type: String,
        required: true,
    },
    text: {
        type: String,
        required: true,
    },
    iconPosition: {
        type: String,
        default: "left",
        validator: (value) => ["left", "right"].includes(value),
    },
    iconSize: {
        type: [String, Number],
        default: 20,
    },
    additionalClasses: {
        type: String,
        default: "",
    },
});

const baseClasses = computed(() => {
    return `flex items-center ${props.additionalClasses}`;
});
</script>

<template>
    <div :class="baseClasses">
        <Icon v-if="icon && iconPosition === 'left'" :icon="icon" class="mr-1.5 mt-0.5 flex-shrink-0" :width="iconSize"
            :height="iconSize" />
        <span class="flex-grow">{{ text }}</span>
        <Icon v-if="icon && iconPosition === 'right'" :icon="icon" class="ml-1.5 mt-0.5 flex-shrink-0" :width="iconSize"
            :height="iconSize" />
    </div>
</template>
