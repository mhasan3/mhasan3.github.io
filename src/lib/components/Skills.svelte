<script lang="ts">
    import { onMount } from "svelte";

    let sectionVisible = $state(false);

    const skillGroups = [
        {
            title: "Languages & Core",
            skills: ["PHP", "JavaScript", "C", "TypeScript", "HTML", "CSS", "SQL"],
        },
        {
            title: "Frameworks & CMS",
            skills: [
                "Laravel",
                "WordPress",
                "Drupal",
                "WooCommerce",
                "Svelte",
                "React",
            ],
        },
        {
            title: "Tools & DevOps",
            skills: ["Git", "Docker", "npm", "Composer", "REST APIs", "MySQL"],
        },
        {
            title: "Platforms",
            skills: ["Pantheon", "Cloudways", "Linode", "Vercel", "Cloudflare"],
        },
    ];

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                entries.forEach((entry) => {
                    if (entry.isIntersecting) sectionVisible = true;
                });
            },
            { threshold: 0.2 },
        );

        const section = document.getElementById("skills");
        if (section) observer.observe(section);

        return () => observer.disconnect();
    });
</script>

<section id="skills" class="section skills-section">
    <div class="container">
        <div class="section-header" class:visible={sectionVisible}>
            <h2>Skills & Expertise</h2>
            <p>Technologies and tools I work with regularly</p>
        </div>

        <div class="skills-grid" class:visible={sectionVisible}>
            {#each skillGroups as group, i}
                <div class="skill-group" style="transition-delay: {i * 100}ms">
                    <h3 class="group-title">{group.title}</h3>
                    <div class="skill-tags">
                        {#each group.skills as skill}
                            <span class="skill-tag">{skill}</span>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .skills-section {
        background: transparent;
    }

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

    .skills-grid {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: var(--space-xl);
        opacity: 0;
        transform: translateY(20px);
        transition: all 0.5s ease 0.1s;
    }

    .skills-grid.visible {
        opacity: 1;
        transform: translateY(0);
    }

    .skill-group {
        padding: var(--space-lg);
        background: var(--color-bg);
        border: 1px solid var(--color-border);
        border-radius: var(--radius-lg);
        transition: all var(--transition-base);
    }

    .skill-group:hover {
        border-color: var(--color-slate-300);
        box-shadow: var(--shadow-md);
    }

    .group-title {
        font-size: 1rem;
        font-weight: 600;
        color: var(--color-text-secondary);
        margin-bottom: var(--space-md);
        text-transform: uppercase;
        letter-spacing: 0.05em;
    }

    .skill-tags {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
    }

    .skill-tag {
        display: inline-flex;
        align-items: center;
        padding: 0.375rem 0.875rem;
        font-size: 0.875rem;
        font-weight: 500;
        color: var(--color-text);
        background: rgba(16, 185, 129, 0.1);
        border-radius: var(--radius-full);
        transition: all var(--transition-fast);
    }

    .skill-tag:hover {
        background: var(--color-slate-200);
    }

    @media (max-width: 768px) {
        .skills-grid {
            grid-template-columns: 1fr;
        }
    }
</style>
