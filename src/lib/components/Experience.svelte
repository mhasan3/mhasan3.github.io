<script lang="ts">
    import { onMount } from "svelte";

    let sectionVisible = $state(false);

    const experiences = [
        {
            title: "Senior Software Engineer",
            company: "bPay Ltd.",
            location: "Dhaka, Bangladesh",
            period: "Jul 2025 - Present",
            highlights: [
                "Contributing to the migration of Laravel 6 to Laravel 12 (Livewire, Filament)",
                "Enhancing and testing existing REST APIs",
                "Developing backend for fintech applications",
            ],
        },
        {
            title: "Senior Software Engineer",
            company: "Adventure Dhaka Ltd.",
            location: "Dhaka, Bangladesh",
            period: "Jan 2025 - Jun 2025",
            highlights: [
                "Contributed to the development of the skyticket OTA platform, built on Laravel",
                "Enhanced and maintained the existing REST API",
                "Participated in architecting a microservice-based architecture",
                "Designed and optimized database schemas for high-traffic applications",
            ],
        },
        {
            title: "Software Engineer",
            company: "Scopic Software",
            location: "Remote (USA)",
            period: "Jun 2022 - Feb 2025",
            highlights: [
                "Developed e-commerce sites utilizing WordPress",
                "Engineered custom plugins based on REST APIs and AngularJS",
                "Performed technical SEO to improve site visibility and performance",
            ],
        },
        {
            title: "Software Engineer & Team Leader",
            company: "Xplantr Ltd.",
            location: "Dhaka, Bangladesh",
            period: "Oct 2017 - Dec 2024",
            highlights: [
                "Led a team of 2-5 developers, serving as primary liaison with clients",
                "Maintained and enhanced existing Laravel-based projects (ERP, reservation systems)",
                "Developed custom Drupal modules and WordPress plugins/themes",
                "Mentored junior developers and instituted bi-monthly growth meetings",
            ],
        },
        {
            title: "Software Engineer",
            company: "Pranon Group",
            location: "Dhaka, Bangladesh",
            period: "Jun 2017 - Sep 2017",
            highlights: [
                "Developed WordPress themes for the Themeforest marketplace",
                "Managed a team of developers",
            ],
        },
        {
            title: "Software Engineer",
            company: "UOUApps",
            location: "Remote (Switzerland)",
            period: "Sep 2014 - May 2017",
            highlights: [
                "Worked as a full-time remote WordPress developer",
                "Built themes for the Themeforest marketplace",
            ],
        },
    ];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) sectionVisible = true;
                });
            },
            { threshold: 0.1 },
        );

        const section = document.getElementById("experience");
        if (section) observer.observe(section);

        return () => observer.disconnect();
    });
</script>

<section id="experience" class="section">
    <div class="container">
        <div class="section-header" class:visible={sectionVisible}>
            <h2>Work Experience</h2>
            <p>
                A decade of professional software engineering and leadership
                roles
            </p>
        </div>

        <div class="timeline" class:visible={sectionVisible}>
            {#each experiences as exp, i}
                <article
                    class="timeline-item"
                    style="transition-delay: {i * 80}ms"
                >
                    <div class="timeline-marker"></div>
                    <div class="timeline-content">
                        <header class="exp-header">
                            <div>
                                <h3 class="exp-title">{exp.title}</h3>
                                <p class="exp-company">
                                    {exp.company}
                                    <span class="exp-location"
                                        >· {exp.location}</span
                                    >
                                </p>
                            </div>
                            <span class="exp-period">{exp.period}</span>
                        </header>
                        <ul class="exp-highlights">
                            {#each exp.highlights as highlight}
                                <li>{highlight}</li>
                            {/each}
                        </ul>
                    </div>
                </article>
            {/each}
        </div>
    </div>
</section>

<style>
    .section-header {
        max-width: 600px;
        margin-bottom: var(--space-2xl);
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.5s ease;
    }

    .section-header.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .section-header p {
        margin-top: var(--space-sm);
    }

    .timeline {
        position: relative;
        max-width: 800px;
        padding-left: var(--space-xl);
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.5s ease 0.1s;
    }

    .timeline.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .timeline::before {
        content: "";
        position: absolute;
        left: 4px;
        top: 8px;
        bottom: 8px;
        width: 1px;
        background: var(--color-border);
    }

    .timeline-item {
        position: relative;
        padding-bottom: var(--space-xl);
    }

    .timeline-item:last-child {
        padding-bottom: 0;
    }

    .timeline-marker {
        position: absolute;
        left: calc(-1 * var(--space-xl) + 1px);
        top: 8px;
        width: 8px;
        height: 8px;
        border-radius: 50%;
        background: var(--color-accent);
    }

    .timeline-content {
        background: var(--color-bg);
        border: 1px solid var(--color-border);
        border-radius: var(--radius-lg);
        padding: var(--space-lg);
        transition: all var(--transition-base);
    }

    .timeline-content:hover {
        border-color: var(--color-slate-300);
        box-shadow: var(--shadow-md);
    }

    .exp-header {
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        gap: var(--space-md);
        margin-bottom: var(--space-md);
    }

    .exp-title {
        font-size: 1.125rem;
        margin-bottom: 0.25rem;
    }

    .exp-company {
        font-size: 0.9375rem;
        font-weight: 500;
        color: var(--color-text-secondary);
        margin: 0;
    }

    .exp-location {
        font-weight: 400;
        color: var(--color-text-muted);
    }

    .exp-period {
        font-size: 0.8125rem;
        font-weight: 500;
        color: var(--color-text-muted);
        white-space: nowrap;
        padding: 0.25rem 0.75rem;
        background: rgba(16, 185, 129, 0.1);
        border-radius: var(--radius-full);
    }

    .exp-highlights {
        list-style: none;
        padding: 0;
        margin: 0;
    }

    .exp-highlights li {
        position: relative;
        padding-left: 1.25rem;
        margin-bottom: 0.5rem;
        font-size: 0.9375rem;
        color: var(--color-text-secondary);
        line-height: 1.6;
    }

    .exp-highlights li:last-child {
        margin-bottom: 0;
    }

    .exp-highlights li::before {
        content: "";
        position: absolute;
        left: 0;
        top: 0.6em;
        width: 4px;
        height: 4px;
        border-radius: 50%;
        background: var(--color-accent);
    }

    @media (max-width: 640px) {
        .exp-header {
            flex-direction: column;
            gap: 0.5rem;
        }

        .timeline {
            padding-left: var(--space-lg);
        }

        .timeline-marker {
            left: calc(-1 * var(--space-lg) + 1px);
        }
    }
</style>
