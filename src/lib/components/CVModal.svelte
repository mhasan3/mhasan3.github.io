<script lang="ts">
    import { onMount } from "svelte";

    interface Props {
        isOpen: boolean;
        onClose: () => void;
    }

    let { isOpen, onClose }: Props = $props();
    let modalRef: HTMLDivElement | undefined = $state();

    const cvPath = "/cv.pdf";

    function handleKeydown(event: KeyboardEvent) {
        if (event.key === "Escape" && isOpen) {
            onClose();
        }
    }

    function handleBackdropClick(event: MouseEvent) {
        if (event.target === modalRef) {
            onClose();
        }
    }

    function handleDownload() {
        const link = document.createElement("a");
        link.href = cvPath;
        link.download = "Mahmudul_Hasan_RUET_CV.pdf";
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
    }

    // Prevent body scroll when modal is open
    $effect(() => {
        if (isOpen) {
            document.body.style.overflow = "hidden";
        } else {
            document.body.style.overflow = "";
        }

        return () => {
            document.body.style.overflow = "";
        };
    });
</script>

<svelte:window on:keydown={handleKeydown} />

{#if isOpen}
    <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
    <div
        class="modal-overlay"
        bind:this={modalRef}
        onclick={handleBackdropClick}
        onkeydown={handleKeydown}
        role="dialog"
        aria-modal="true"
        aria-labelledby="cv-modal-title"
    >
        <div class="modal-container">
            <div class="modal-header">
                <h3 id="cv-modal-title">Curriculum Vitae</h3>
                <div class="modal-actions">
                    <button
                        class="btn-icon download-btn"
                        onclick={handleDownload}
                        aria-label="Download CV"
                        title="Download CV"
                    >
                        <svg
                            viewBox="0 0 24 24"
                            fill="none"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            width="20"
                            height="20"
                        >
                            <path
                                d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"
                            />
                            <polyline points="7 10 12 15 17 10" />
                            <line x1="12" y1="15" x2="12" y2="3" />
                        </svg>
                        <span>Download</span>
                    </button>
                    <button
                        class="btn-icon close-btn"
                        onclick={onClose}
                        aria-label="Close modal"
                    >
                        <svg
                            viewBox="0 0 24 24"
                            fill="none"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            width="20"
                            height="20"
                        >
                            <line x1="18" y1="6" x2="6" y2="18" />
                            <line x1="6" y1="6" x2="18" y2="18" />
                        </svg>
                    </button>
                </div>
            </div>
            <div class="modal-body">
                <iframe src={cvPath} title="CV Preview" class="cv-viewer"
                ></iframe>
            </div>
        </div>
    </div>
{/if}

<style>
    .modal-overlay {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: rgba(0, 0, 0, 0.6);
        backdrop-filter: blur(4px);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
        padding: var(--space-md);
        animation: fadeIn 0.2s ease;
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    .modal-container {
        background: var(--color-bg);
        border-radius: var(--radius-xl);
        width: 100%;
        max-width: 900px;
        max-height: 90vh;
        display: flex;
        flex-direction: column;
        box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25);
        animation: slideUp 0.3s ease;
        overflow: hidden;
    }

    @keyframes slideUp {
        from {
            opacity: 0;
            transform: translateY(20px) scale(0.98);
        }
        to {
            opacity: 1;
            transform: translateY(0) scale(1);
        }
    }

    .modal-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: var(--space-md) var(--space-lg);
        border-bottom: 1px solid var(--color-border);
        background: var(--color-bg-alt);
    }

    .modal-header h3 {
        font-size: 1.25rem;
        font-weight: 600;
        color: var(--color-text);
        margin: 0;
    }

    .modal-actions {
        display: flex;
        align-items: center;
        gap: var(--space-xs);
    }

    .btn-icon {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
        padding: 0.5rem 1rem;
        font-family: var(--font-body);
        font-size: 0.875rem;
        font-weight: 500;
        color: var(--color-text-secondary);
        background: transparent;
        border: 1px solid var(--color-border);
        border-radius: var(--radius-md);
        cursor: pointer;
        transition: all var(--transition-fast);
    }

    .btn-icon:hover {
        background: var(--color-bg);
        border-color: var(--color-slate-300);
        color: var(--color-text);
    }

    .download-btn {
        background: var(--color-slate-900);
        color: white;
        border-color: var(--color-slate-900);
    }

    .download-btn:hover {
        background: var(--color-slate-800);
        border-color: var(--color-slate-800);
        color: white;
    }

    .close-btn {
        padding: 0.5rem;
    }

    .modal-body {
        flex: 1;
        overflow: hidden;
        background: var(--color-slate-100);
    }

    .cv-viewer {
        width: 100%;
        height: 70vh;
        border: none;
        display: block;
    }

    @media (max-width: 768px) {
        .modal-overlay {
            padding: 0;
        }

        .modal-container {
            max-width: 100%;
            max-height: 100vh;
            border-radius: 0;
            height: 100%;
        }

        .modal-header {
            padding: var(--space-sm) var(--space-md);
        }

        .modal-header h3 {
            font-size: 1rem;
        }

        .download-btn span {
            display: none;
        }

        .download-btn {
            padding: 0.5rem;
        }

        .cv-viewer {
            height: calc(100vh - 60px);
        }
    }
</style>
