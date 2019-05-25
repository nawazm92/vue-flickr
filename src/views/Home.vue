<template>
    <div>
        <hero-section
            backgroundImage="homepage-hero.jpg"
            title="Welcome to VueFlickrDemo"
            subtitle="A simple photo app" />
        <div class="wrapper">
        </div>
    </div>
</template>

<script>
import HeroSection from '@/components/HeroSection';

export default {
    name: 'home',
    components: {
        HeroSection
    }
};
</script>