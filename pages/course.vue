
<template>
    <div class="container">
        <div class="header m-10">
            <h1 style="text-align: center">We're building a course app</h1>
        </div>

        <div class="flex flex-row h-screen">
            <nav class="w-3/12  px-10 py-10 border flex flex-col shadow-1xl ">
                <div class="logo">
                    <svg width="107" height="20" viewBox="0 0 107 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M10.042 20C4.45876 20 0 15.804 0 10.06C0 4.236 4.51342 0 10.042 0C15.5705 0 20.1113 4.236 20.1113 10.06C20.1113 15.804 15.6213 20 10.042 20ZM15.4729 10C15.4729 6.58 13.0327 4.108 10.0615 4.108C7.09029 4.108 4.65398 6.58 4.65398 10C4.65398 13.42 7.06686 15.864 10.0693 15.864C13.0717 15.864 15.4729 13.436 15.4729 10ZM32.0508 20C26.4675 20 22.0088 15.804 22.0088 10.06C22.0166 4.236 26.5339 0 32.0586 0C37.5832 0 42.1279 4.236 42.1279 10.06C42.1279 15.804 37.6418 20 32.0586 20H32.0508ZM37.4934 10C37.4934 6.58 35.0532 4.108 32.0781 4.108C29.103 4.108 26.6745 6.58 26.6745 10C26.6745 13.42 29.0835 15.864 32.0859 15.864C35.0883 15.864 37.5012 13.436 37.5012 10H37.4934ZM54.0673 20C48.488 20 44.0293 15.804 44.0293 10.06C44.0371 4.236 48.5505 0 54.0752 0C59.5998 0 64.1445 4.236 64.1445 10.06C64.1445 15.804 59.6584 20 54.0752 20H54.0673ZM59.51 10C59.51 6.58 57.0698 4.108 54.0986 4.108C51.1274 4.108 48.6833 6.58 48.6833 10C48.6833 13.42 51.104 15.864 54.1259 15.864C57.1479 15.864 59.5178 13.436 59.5178 10H59.51ZM79.957 19.772L70.9146 7.156H70.8014L70.9966 19.772H66.8189V0.236H70.7233L79.8126 12.82H79.8946L79.7111 0.236H83.8926V19.772H79.957ZM96.5895 20C91.0102 20 86.5476 15.804 86.5476 10.06C86.5554 4.236 91.0727 0 96.5974 0C102.122 0 106.667 4.236 106.667 10.06C106.667 15.804 102.181 20 96.5974 20H96.5895ZM102.032 10C102.032 6.58 99.592 4.108 96.6169 4.108C93.6418 4.108 91.2172 6.58 91.2172 10C91.2172 13.42 93.6301 15.864 96.6286 15.864C99.6271 15.864 102.04 13.436 102.04 10H102.032Z"
                            fill="currentColor">
                        </path>
                    </svg>
                </div>
                <div class="content">
                    <div v-for="chapter in chapters" :key="chapter.slug" class="space-y-1 mb-4 flex flex-col">
                        <h4 class="mt-10 mb-5 font-bold">{{ chapter.title }}</h4>
                        <NuxtLink v-for="(lesson, index) in chapter.lessons" :key="lesson.slug" :to="lesson.path">
                            <span>{{ index + 1 }}.</span>
                            <span>{{ lesson.title }}</span>
                        </NuxtLink>
                    </div>
                </div>
            </nav>
            <section class="w-9/12 mx-2  px-10 py-10 border flex flex-col shadow-1xl">
                <NuxtPage />
            </section>
        </div>
    </div>
</template>

<script setup>
const { chapters } = useCourse();
</script>


<style scroped>
.router-link-active {
    @apply text-blue-900;
}

.container {
    max-width: 1240px;
    margin: 0 auto;
}
</style>