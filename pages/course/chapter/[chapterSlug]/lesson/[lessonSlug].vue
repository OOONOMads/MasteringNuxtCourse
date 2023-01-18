<template>
    <div>
        <p class="mb-5">Lesson {{ chapter.number }} - {{ lesson.number }}</p>
        <h2 class="font-bold mb-5">{{ lesson.title }}</h2>

        <NuxtLink class="mb-5 block text-blue-900" v-if="lesson.downloadUrl" :to="lesson.downloadUrl">Download Video
        </NuxtLink>

        <p class="max-w-2xl">{{ lesson.text }}</p>

        <LessonCompleteButton :model-value="isLessonComplete" @update:model-value="toggleComplete" />
        <VideoPlayer v-if="lesson.videoId" :videoId="lesson.videoId" />
    </div>
</template>

<script setup>
import VideoPlayer from '~~/components/VideoPlayer.vue';

const course = useCourse();
const battery = useBattery();
const route = useRoute();

const chapter = computed(() => {
    return course.chapters.find(
        (chapter) => chapter.slug === route.params.chapterSlug
    )
});

const lesson = computed(() => {
    return chapter.value.lessons.find(
        (lesson) => lesson.slug === route.params.lessonSlug
    );
});

const title = computed(() => {
    return `${lesson.value.title} - ${course.title}`;
});

useHead({
    title: title,
})

const progress = useLocalStorage('progress', []);

const isLessonComplete = computed(() => {
    if (!progress.value[chapter.value.number - 1]) {
        return false;
    }
    if (
        !progress.value[chapter.value.number - 1][
        lesson.value.number - 1
        ]
    ) {
        return false;
    }
    return progress.value[chapter.value.number - 1][
        lesson.value.number - 1
    ];
});

const toggleComplete = () => {
    if (!progress.value[chapter.value.number - 1]) {
        progress.value[chapter.value.number - 1] = [];
    }
    progress.value[chapter.value.number - 1][lesson.value.number - 1] = !isLessonComplete.value;
};
</script>