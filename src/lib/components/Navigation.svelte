<script lang="ts">
    import { onMount } from "svelte";

    let activeSection = $state("home");
    let scrolled = $state(false);
    let mobileMenuOpen = $state(false);

    const navItems = [
        { id: "home", label: "Home" },
        { id: "about", label: "About" },
        { id: "experience", label: "Experience" },
        { id: "skills", label: "Skills" },
        { id: "contact", label: "Contact" },
    ];

    function scrollToSection(sectionId: string) {
        const element = document.getElementById(sectionId);
        if (element) {
            element.scrollIntoView({ behavior: "smooth" });
            activeSection = sectionId;
            mobileMenuOpen = false;
        }
    }

    onMount(() => {
        const handleScroll = () => {
            scrolled = window.scrollY > 20;

            const sections = navItems.map((item) =>
                document.getElementById(item.id),
            );
            const scrollPosition = window.scrollY + 100;

            sections.forEach((section, index) => {
                if (section) {
                    const top = section.offsetTop;
                    const bottom = top + section.offsetHeight;

                    if (scrollPosition >= top && scrollPosition < bottom) {
                        activeSection = navItems[index].id;
                    }
                }
            });
        };

        window.addEventListener("scroll", handleScroll);
        return () => window.removeEventListener("scroll", handleScroll);
    });
</script>

<nav class="nav" class:scrolled>
    <div class="nav-content">
        <button class="nav-logo" onclick={() => scrollToSection("home")}>
            MH<span class="text-accent">.</span>
        </button>

        <ul class="nav-menu" class:open={mobileMenuOpen}>
            {#each navItems as item}
                <li>
                    <button
                        class="nav-link"
                        class:active={activeSection === item.id}
                        onclick={() => scrollToSection(item.id)}
                    >
                        {item.label}
                    </button>
                </li>
            {/each}
        </ul>

        <button
            class="mobile-toggle"
            onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
            aria-label="Toggle menu"
        >
            <span class:open={mobileMenuOpen}></span>
        </button>
    </div>
</nav>

<style>
    .nav {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        z-index: 100;
        padding: var(--space-sm) 0;
        background: rgba(255, 255, 255, 0.9);
        backdrop-filter: blur(12px);
        -webkit-backdrop-filter: blur(12px);
        transition: all var(--transition-base);
    }

    .nav.scrolled {
        border-bottom: 1px solid var(--color-border);
        box-shadow: var(--shadow-sm);
    }

    .nav-content {
        max-width: var(--max-width);
        margin: 0 auto;
        padding: 0 var(--space-md);
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .nav-logo {
        font-family: var(--font-heading);
        font-size: 1.5rem;
        font-weight: 700;
        color: var(--color-text);
        background: none;
        border: none;
        cursor: pointer;
        letter-spacing: -0.02em;
    }

    .nav-menu {
        display: flex;
        gap: var(--space-xs);
        list-style: none;
    }

    .nav-link {
        background: none;
        border: none;
        color: var(--color-text-secondary);
        font-family: var(--font-body);
        font-size: 0.9375rem;
        font-weight: 500;
        cursor: pointer;
        padding: 0.5rem 0.875rem;
        border-radius: var(--radius-md);
        transition: all var(--transition-fast);
    }

    .nav-link:hover {
        color: var(--color-text);
        background: var(--color-bg-alt);
    }

    .nav-link.active {
        color: var(--color-accent);
        background: rgba(16, 185, 129, 0.1);
    }

    .mobile-toggle {
        display: none;
        background: none;
        border: none;
        width: 24px;
        height: 24px;
        cursor: pointer;
        position: relative;
    }

    .mobile-toggle span,
    .mobile-toggle span::before,
    .mobile-toggle span::after {
        display: block;
        position: absolute;
        width: 24px;
        height: 2px;
        background: var(--color-text);
        transition: all var(--transition-fast);
    }

    .mobile-toggle span {
        top: 50%;
        transform: translateY(-50%);
    }

    .mobile-toggle span::before {
        content: "";
        top: -7px;
    }

    .mobile-toggle span::after {
        content: "";
        top: 7px;
    }

    .mobile-toggle span.open {
        background: transparent;
    }

    .mobile-toggle span.open::before {
        top: 0;
        transform: rotate(45deg);
    }

    .mobile-toggle span.open::after {
        top: 0;
        transform: rotate(-45deg);
    }

    @media (max-width: 768px) {
        .mobile-toggle {
            display: block;
        }

        .nav-menu {
            position: fixed;
            top: var(--nav-height);
            left: 0;
            right: 0;
            background: var(--color-bg);
            border-bottom: 1px solid var(--color-border);
            flex-direction: column;
            padding: var(--space-sm);
            gap: 0;
            transform: translateY(-100%);
            opacity: 0;
            pointer-events: none;
            transition: all var(--transition-base);
        }

        .nav-menu.open {
            transform: translateY(0);
            opacity: 1;
            pointer-events: all;
        }

        .nav-link {
            width: 100%;
            text-align: left;
            padding: var(--space-sm);
        }
    }
</style>
