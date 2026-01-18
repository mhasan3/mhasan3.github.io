<script lang="ts">
    import { onMount } from "svelte";

    let sectionVisible = $state(false);

    const highlights = [
        { label: "10+ Years", description: "Professional Experience" },
        { label: "CSM®", description: "Certified ScrumMaster" },
        { label: "B.Sc in CSE", description: "RUET, Bangladesh" },
    ];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) {
                        sectionVisible = true;
                    }
                });
            },
            { threshold: 0.2 },
        );

        const section = document.getElementById("about");
        if (section) observer.observe(section);

        return () => observer.disconnect();
    });
</script>

<section id="about" class="section about-section">
    <div class="container">
        <div class="about-content" class:visible={sectionVisible}>
            <div class="section-header">
                <h2>About Me</h2>
            </div>

            <div class="about-body">
                <p>
                    A detail-oriented Senior Software Engineer with over a
                    decade of experience specializing in PHP-driven web
                    development. I have proven expertise in building and
                    managing WordPress e-commerce and multisite platforms,
                    alongside designing and implementing robust Laravel APIs.
                </p>

                <p>
                    My skills span system architecture, database optimization,
                    and third-party API integration. As a Certified
                    ScrumMaster®, I have a track record of leading development
                    teams, mentoring junior developers, and successfully
                    managing projects from conception to deployment.
                </p>

                <div class="highlights-grid">
                    {#each highlights as item, i}
                        <div
                            class="highlight-item"
                            style="transition-delay: {i * 100}ms"
                        >
                            <span class="highlight-value">{item.label}</span>
                            <span class="highlight-label"
                                >{item.description}</span
                            >
                        </div>
                    {/each}
                </div>
            </div>
        </div>
    </div>
</section>

<style>
    .about-section {
        background: transparent;
    }

    .about-content {
        max-width: 720px;
        opacity: 0;
        transform: translateY(24px);
        transition: all 0.6s ease;
    }

    .about-content.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .about-body p {
        margin-bottom: var(--space-md);
    }

    .about-body p:last-of-type {
        margin-bottom: var(--space-xl);
    }

    .highlights-grid {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        gap: var(--space-md);
        padding-top: var(--space-lg);
        border-top: 1px solid var(--color-border);
    }

    .highlight-item {
        display: flex;
        flex-direction: column;
        gap: 0.25rem;
    }

    .highlight-value {
        font-family: var(--font-heading);
        font-size: 1.5rem;
        font-weight: 600;
        color: var(--color-text);
        letter-spacing: -0.02em;
    }

    .highlight-label {
        font-size: 0.875rem;
        color: var(--color-text-muted);
    }

    @media (max-width: 768px) {
        .highlights-grid {
            grid-template-columns: repeat(2, 1fr);
        }
    }

    @media (max-width: 480px) {
        .highlights-grid {
            grid-template-columns: 1fr 1fr;
            gap: var(--space-sm);
        }
    }
</style>
