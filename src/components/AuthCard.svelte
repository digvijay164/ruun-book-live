<script>
    import { onMount } from "svelte";
    import { BrainCircuit } from "lucide-svelte";
    import { gsap } from "gsap";

    let { title, subtitle, children } = $props();
    let cardElement;

    onMount(() => {
        import("gsap").then(({ gsap }) => {
            gsap.fromTo(
                cardElement,
                { y: 50, opacity: 0, scale: 0.95 },
                {
                    y: 0,
                    opacity: 1,
                    scale: 1,
                    duration: 0.6,
                    ease: "back.out(1.2)",
                },
            );
        });
    });
</script>

<div
    class="min-h-screen flex items-center justify-center p-6 relative overflow-hidden bg-black"
>
    <div
        class="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjAiIGhlaWdodD0iMjAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PGNpcmNsZSBjeD0iMSIgY3k9IjEiIHI9IjEiIGZpbGw9InJnYmEoMjU1LDI1NSwyNTUsMC4wNSkiLz48L3N2Zz4=')] opacity-50"
    ></div>
    <div
        class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[30rem] h-[30rem] bg-blue-600/20 blur-[100px] rounded-full pointer-events-none"
    ></div>

    <div
        bind:this={cardElement}
        class="w-full max-w-md relative z-10 bg-slate-950/80 backdrop-blur-xl border border-white/10 rounded-3xl p-8 shadow-2xl"
    >
        <div class="text-center mb-8">
            <a
                href="/"
                class="inline-flex items-center justify-center p-3 rounded-2xl bg-slate-900 border border-white/5 mb-6 hover:bg-slate-800 transition-colors"
            >
                <BrainCircuit class="w-8 h-8 text-blue-500" />
            </a>
            <h1 class="text-2xl font-bold text-white mb-2">{title}</h1>
            <p class="text-slate-400 text-sm">{subtitle}</p>
        </div>

        {@render children()}
    </div>
</div>
