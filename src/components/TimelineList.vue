<script setup>
import IconWrapper from "@/components/IconWrapper.vue";
import ItemList from "@/components/ItemList.vue";

defineProps({
    activities: {
        type: Array,
        default: () => [],
    },
});
</script>

<template>
    <ol class="relative ms-4 border-s-2 border-primary-content">
        <li v-for="(activity, index) in activities" :key="index" class="ms-10"
            :class="{ 'mb-10': index !== activities.length - 1 }">
            <span class="absolute -start-3 flex w-6 items-center justify-center">
                <IconWrapper :icon="activity.icon" />
            </span>
            <h3 class="text-xl font-semibold text-gray-900">
                {{ activity.title }}
            </h3>
            <span class="text-gray-500">{{ activity.period }}</span>
            <div class="pt-2" v-if="activity.jobdesk?.length > 0">
                <ItemList :items="activity.jobdesk" :column="1" />
            </div>
        </li>
    </ol>
</template>
