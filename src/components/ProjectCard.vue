<script setup>
import { ref } from "vue";
import FallbackImage from "@/components/FallbackImage.vue";
import IconText from "@/components/IconText.vue";
import IconWrapper from "@/components/IconWrapper.vue";
import ExternalLink from "@/components/ExternalLink.vue";

defineProps({
    image: {
        type: String,
    },
    title: {
        type: String,
        required: true,
    },
    tools: {
        type: Object,
        required: true,
    },
    description: {
        type: String,
        required: true,
    },
    url: {
        type: String,
    },
});

const showFallback = ref(false);

const handleImageError = () => {
    showFallback.value = true;
};
</script>

<template>
    <div class="flex h-full flex-col overflow-hidden rounded-lg border border-gray-200">
        <img v-if="!showFallback" :src="image" loading="lazy" :alt="title" @error="handleImageError"
            class="aspect-video object-cover object-top transition duration-200" />
        <FallbackImage v-else :title="title" />

        <div class="flex flex-grow flex-col justify-between gap-1 px-7 py-5">
            <div class="mb-10 flex-grow">
                <h3 class="text-xl font-semibold text-gray-900">
                    {{ title }}
                </h3>
                <p class="pt-4 text-gray-600">{{ description }}</p>
            </div>
            <div class="flex items-center justify-between">
                <div class="flex gap-2">
                    <div v-for="(url, tool) in tools" :key="tool">
                        <ExternalLink :url="url">
                            <IconWrapper :icon="`simple-icons:${tool}`" :size="20" />
                        </ExternalLink>
                    </div>
                </div>
                <ExternalLink v-if="url" :url="url" class="font-semibold text-primary hover:underline">
                    <IconText :icon="'heroicons:arrow-top-right-on-square-16-solid'" :text="'Explore'"
                        :iconPosition="'right'" />
                </ExternalLink>
            </div>
        </div>
    </div>
</template>
