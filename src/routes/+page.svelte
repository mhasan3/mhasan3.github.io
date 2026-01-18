<script lang="ts">
    import Navigation from "$lib/components/Navigation.svelte";
    import Hero from "$lib/components/Hero.svelte";
    import About from "$lib/components/About.svelte";
    import Experience from "$lib/components/Experience.svelte";
    import Skills from "$lib/components/Skills.svelte";
    import Contact from "$lib/components/Contact.svelte";
</script>

<svelte:head>
    <title>Md. Mahmudul Hasan | Senior Software Engineer</title>
    <meta
        name="description"
        content="Senior Software Engineer with 10+ years of experience in PHP, Laravel, and WordPress. Specializing in fintech, system architecture, and team leadership."
    />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link
        rel="preconnect"
        href="https://fonts.gstatic.com"
        crossorigin="anonymous"
    />
    <link
        href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Outfit:wght@500;600;700&display=swap"
        rel="stylesheet"
    />
</svelte:head>

<!-- Floating Particles - 32 particles -->
<div class="particles" aria-hidden="true">
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
    <div class="particle"></div>
</div>

<div class="app">
    <Navigation />
    <main>
        <Hero />
        <About />
        <Experience />
        <Skills />
        <Contact />
    </main>
</div>

<style>
    .app {
        position: relative;
        width: 100%;
        min-height: 100vh;
    }

    main {
        position: relative;
        width: 100%;
    }
</style>
