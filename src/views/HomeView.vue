<script setup>
import { RouterLink } from "vue-router";

import data from "@/assets/data.json";

import ExternalLink from "@/components/ExternalLink.vue";
import IconText from "@/components/IconText.vue";
import PrimaryButton from "@/components/PrimaryButton.vue";
import ProfileCard from "@/components/ProfileCard.vue";
import ProjectCard from "@/components/ProjectCard.vue";
import SecondaryButton from "@/components/SecondaryButton.vue";
import SectionTitle from "@/components/SectionTitle.vue";
import TimelineList from "@/components/TimelineList.vue";

const { profile, education, technical_skills, work_experience, projects } =
    data;
</script>

<template>
    <!-- Hero -->
    <section id="hero" class="px-6 py-7 md:px-10 md:py-12">
        <div
            class="mx-auto flex max-w-screen-xl flex-col items-center gap-6 lg:flex-row-reverse lg:items-start lg:gap-14">
            <!-- Profile Picture -->
            <img :src="profile.image" alt="Profile" class="h-32 rounded-full md:h-56" />

            <!-- Bio -->
            <div class="flex flex-col gap-6">
                <h1 class="text-center text-3xl font-bold text-gray-900 md:text-5xl lg:text-start">
                    Hi there! I'm
                    <span class="block text-primary underline md:inline">{{ profile.name }}</span>
                </h1>
                <p class="text-justify leading-relaxed text-lg text-gray-700 lg:text-start">
                    {{ profile.bio }}
                </p>
                <div class="flex items-center justify-center gap-6 lg:justify-start">
                    <RouterLink :to="{ path: '/', hash: '#contact' }">
                        <PrimaryButton>Get in touch</PrimaryButton>
                    </RouterLink>
                    <ExternalLink :url="`${profile.resume_url}`" class="font-semibold text-primary hover:underline">
                        <IconText :icon="'heroicons:arrow-top-right-on-square-16-solid'" :iconPosition="'right'"
                            :text="'Explore my resume'" />
                    </ExternalLink>
                </div>
            </div>
        </div>
    </section>

    <!-- About -->
    <section id="about" class="bg-primary-light px-6 py-7 md:px-10 md:py-12">
        <div class="mx-auto flex max-w-screen-xl flex-col gap-14 md:flex-row md:justify-between lg:gap-20">
            <!-- Background -->
            <div class="md:w-1/2 flex w-full flex-col gap-14">
                <!-- Education -->
                <div id="education">
                    <SectionTitle class="pb-8">Education</SectionTitle>
                    <ProfileCard :icon="education.icon" :title="education.institution" :sub_title="education.degree"
                        :description="education.thesis" :list_title="'Relevant subjects:'" :items="education.subjects"
                        :column="1" />
                </div>

                <!-- Skills -->
                <div id="technical-skills">
                    <SectionTitle class="pb-8">Technical Skills</SectionTitle>
                    <div v-for="(technical_skill, index) in technical_skills" :key="index">
                        <ProfileCard :icon="technical_skill.icon" :title="technical_skill.category"
                            :sub_title="technical_skill.degree" :description="technical_skill.description"
                            :items="technical_skill.skills"
                            :class="`${index === technical_skills.length - 1 ? '' : 'pb-8'}`" />
                    </div>
                </div>
            </div>

            <!-- Work Experience -->
            <div id="work-experience" class="md:w-1/2 w-full">
                <SectionTitle class="pb-8">Work Experience</SectionTitle>
                <TimelineList :activities="work_experience" />
            </div>
        </div>
    </section>

    <!-- Projects -->
    <section id="projects" class="bg-primary-light px-6 pb-20 pt-7 md:px-10 md:pb-24 md:pt-12">
        <div class="mx-auto max-w-screen-xl">
            <SectionTitle>Project Showcase</SectionTitle>
            <p class="pt-3 text-gray-700">
                These are projects I've developed, providing effective solutions to diverse problems.
            </p>

            <div class="flex flex-col items-center pt-8">
                <div class="grid gap-x-7 gap-y-7 pt-3 md:grid-cols-2 lg:grid-cols-3">
                    <!-- Project -->
                    <ProjectCard v-for="(project, index) in projects" :key="index" :image="project.image"
                        :tools="project.tools" :title="project.title" :description="project.description"
                        :url="project.url" />
                </div>
            </div>
        </div>
    </section>

    <!-- CTA -->
    <section id="contact" class="bg-primary px-6 py-16 md:px-10">
        <div class="mx-auto flex max-w-screen-xl flex-col items-center justify-center gap-4">
            <h2 class="text-center text-4xl font-bold text-white">
                Let's Collaborate!
            </h2>
            <p class="text-center text-lg text-white">
                Ready to discuss projects, ideas, or just connect? Feel free to
                reach out to me
            </p>
            <ExternalLink :url="`mailto:${profile.email}`" class="mt-4">
                <SecondaryButton>
                    <IconText :icon="'material-symbols:mail'" :text="profile.email" :iconSize="28" />
                </SecondaryButton>
            </ExternalLink>
        </div>
    </section>
</template>
