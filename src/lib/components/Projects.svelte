<script lang="ts">
    import { onMount } from "svelte";

    let sectionVisible = $state(false);

    const projects = [
        {
            title: "Analytics Dashboard",
            description:
                "A comprehensive analytics platform with real-time data visualization, interactive charts, and custom reporting features.",
            image: "/project1.png",
            tags: ["React", "TypeScript", "D3.js", "Node.js"],
            link: "#",
        },
        {
            title: "E-Commerce Platform",
            description:
                "Modern e-commerce solution with seamless checkout, inventory management, and personalized shopping experience.",
            image: "/project2.png",
            tags: ["Vue", "Tailwind", "Stripe", "MongoDB"],
            link: "#",
        },
        {
            title: "Creative Portfolio",
            description:
                "Stunning portfolio website with dynamic animations, smooth transitions, and engaging user interactions.",
            image: "/project3.png",
            tags: ["Svelte", "CSS", "Animation", "Design"],
            link: "#",
        },
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

        const section = document.getElementById("projects");
        if (section) observer.observe(section);

        return () => observer.disconnect();
    });
</script>

<section id="projects" class="section projects-section">
    <div class="container">
        <div
            class="section-title"
            class:scroll-reveal={!sectionVisible}
            class:revealed={sectionVisible}
        >
            <h2>Featured <span class="text-gradient">Projects</span></h2>
            <p>A showcase of my recent work and creative solutions</p>
        </div>

        <div class="projects-grid">
            {#each projects as project, index}
                <div
                    class="project-card glass-card"
                    class:scroll-reveal={!sectionVisible}
                    class:revealed={sectionVisible}
                    class:stagger-1={index === 1}
                    class:stagger-2={index === 2}
                >
                    <div class="project-image">
                        <img src={project.image} alt={project.title} />
                        <div class="project-overlay">
                            <a href={project.link} class="btn btn-primary">
                                View Project
                                <svg
                                    xmlns="http://www.w3.org/2000/svg"
                                    width="20"
                                    height="20"
                                    viewBox="0 0 24 24"
                                    fill="none"
                                    stroke="currentColor"
                                    stroke-width="2"
                                    stroke-linecap="round"
                                    stroke-linejoin="round"
                                >
                                    <line x1="7" y1="17" x2="17" y2="7"></line>
                                    <polyline points="7 7 17 7 17 17"
                                    ></polyline>
                                </svg>
                            </a>
                        </div>
                    </div>

                    <div class="project-content">
                        <h3>{project.title}</h3>
                        <p>{project.description}</p>

                        <div class="project-tags">
                            {#each project.tags as tag}
                                <span class="tag">{tag}</span>
                            {/each}
                        </div>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</section>

<style>
    .projects-section {
        position: relative;
        overflow: hidden;
    }

    .projects-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
        gap: var(--space-xl);
    }

    .project-card {
        padding: 0;
        overflow: hidden;
        transition: all var(--transition-base);
    }

    .project-card:hover {
        transform: translateY(-4px);
    }

    .project-image {
        position: relative;
        width: 100%;
        height: 280px;
        overflow: hidden;
        background: var(--color-bg-tertiary);
    }

    .project-image img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: transform var(--transition-slow);
    }

    .project-card:hover .project-image img {
        transform: scale(1.05);
    }

    .project-overlay {
        position: absolute;
        inset: 0;
        background: linear-gradient(
            180deg,
            transparent 0%,
            rgba(10, 10, 15, 0.9) 100%
        );
        display: flex;
        align-items: center;
        justify-content: center;
        opacity: 0;
        transition: opacity var(--transition-base);
    }

    .project-card:hover .project-overlay {
        opacity: 1;
    }

    .project-overlay .btn {
        transform: translateY(20px);
        transition: transform var(--transition-base);
    }

    .project-card:hover .project-overlay .btn {
        transform: translateY(0);
    }

    .project-content {
        padding: var(--space-lg);
    }

    .project-content h3 {
        margin-bottom: var(--space-sm);
        font-size: 1.5rem;
    }

    .project-content p {
        margin-bottom: var(--space-md);
        color: var(--color-text-secondary);
        font-size: 0.95rem;
    }

    .project-tags {
        display: flex;
        flex-wrap: wrap;
        gap: var(--space-xs);
    }

    .tag {
        padding: 0.375rem 0.75rem;
        background: rgba(168, 85, 247, 0.15);
        border: 1px solid rgba(168, 85, 247, 0.3);
        border-radius: var(--radius-full);
        color: var(--color-primary-light);
        font-size: 0.875rem;
        font-weight: 500;
        transition: all var(--transition-base);
    }

    .tag:hover {
        background: rgba(168, 85, 247, 0.25);
        border-color: var(--color-primary);
    }

    @media (max-width: 768px) {
        .projects-grid {
            grid-template-columns: 1fr;
        }
    }
</style>
