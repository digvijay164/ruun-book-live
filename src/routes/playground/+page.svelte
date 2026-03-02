<script>
    import { onMount } from "svelte";
    import { user, logout } from "../../stores/auth";
    import { goto } from "$app/navigation";
    import {
        Network,
        Database,
        BrainCircuit,
        Play,
        Settings,
        Menu,
    } from "lucide-svelte";
    import { gsap } from "gsap";

    let isSidebarOpen = true;

    // Optional: Protect route (blueirect if no user, but skip for now to let user explore UI if they go direct)
    // onMount(() => {
    //    if (!$user) {
    //        goto('/login');
    //    }
    // });
</script>

<div
    class="h-screen w-full bg-black flex flex-col overflow-hidden text-zinc-200 font-sans"
>
    <!-- Topbar -->
    <header
        class="h-14 border-b border-white/5 bg-zinc-950/50 flex items-center justify-between px-4 z-20 backdrop-blur-md"
    >
        <div class="flex items-center gap-4">
            <!-- svelte-ignore a11y_consider_explicit_label -->
            <button
                onclick={() => (isSidebarOpen = !isSidebarOpen)}
                class="p-2 hover:bg-white/5 rounded-lg transition-colors"
            >
                <Menu class="w-5 h-5 text-zinc-400" />
            </button>
            <div class="flex items-center gap-2">
                <BrainCircuit class="w-5 h-5 text-red-500" />
                <span class="font-bold text-sm text-white"
                    >Project: Cblueit Card Fraud Detection</span
                >
            </div>
            <div
                class="px-2 py-0.5 rounded bg-red-500/10 border border-red-500/20 text-[10px] font-bold text-red-400 uppercase tracking-widest ml-2"
            >
                Saved
            </div>
        </div>

        <div class="flex items-center gap-3">
            <button
                class="bg-red-600 hover:bg-red-500 text-white px-4 py-1.5 rounded-lg text-sm font-bold flex items-center gap-2 transition-colors"
            >
                <Play class="w-4 h-4" /> Train Model
            </button>
            <div
                class="w-8 h-8 rounded-full bg-zinc-900 border border-white/10 flex items-center justify-center text-sm font-bold text-zinc-300 ml-4 cursor-pointer hover:bg-zinc-800"
                title="Logout"
                onclick={logout}
            >
                {$user ? $user.name.charAt(0).toUpperCase() : "U"}
            </div>
        </div>
    </header>

    <div class="flex-1 flex overflow-hidden">
        <!-- Sidebar (Nodes List) -->
        {#if isSidebarOpen}
            <aside
                class="w-64 border-r border-white/5 bg-zinc-950/30 flex flex-col overflow-y-auto transform transition-all"
            >
                <div class="p-4 border-b border-white/5">
                    <h3
                        class="text-xs font-bold text-zinc-500 uppercase tracking-wider mb-4"
                    >
                        Components
                    </h3>

                    <div class="space-y-6">
                        <div>
                            <div
                                class="text-[10px] font-bold text-zinc-600 uppercase mb-2"
                            >
                                Data
                            </div>
                            <div
                                class="flex items-center gap-3 p-2 bg-zinc-900/50 hover:bg-zinc-900 border border-white/5 rounded-lg cursor-grab active:cursor-grabbing transition-colors"
                            >
                                <Database class="w-4 h-4 text-red-400" />
                                <span class="text-xs font-medium text-zinc-300"
                                    >CSV Dataset</span
                                >
                            </div>
                        </div>

                        <div>
                            <div
                                class="text-[10px] font-bold text-zinc-600 uppercase mb-2"
                            >
                                Layers
                            </div>
                            <div class="space-y-2">
                                <div
                                    class="flex items-center gap-3 p-2 bg-zinc-900/50 hover:bg-zinc-900 border border-white/5 rounded-lg cursor-grab active:cursor-grabbing transition-colors"
                                >
                                    <Network class="w-4 h-4 text-red-500" />
                                    <span
                                        class="text-xs font-medium text-zinc-300"
                                        >Dense Layer</span
                                    >
                                </div>
                                <div
                                    class="flex items-center gap-3 p-2 bg-zinc-900/50 hover:bg-zinc-900 border border-white/5 rounded-lg cursor-grab active:cursor-grabbing transition-colors"
                                >
                                    <Network class="w-4 h-4 text-red-500" />
                                    <span
                                        class="text-xs font-medium text-zinc-300"
                                        >Dropout Layer</span
                                    >
                                </div>
                            </div>
                        </div>

                        <div>
                            <div
                                class="text-[10px] font-bold text-zinc-600 uppercase mb-2"
                            >
                                Evaluation
                            </div>
                            <div
                                class="flex items-center gap-3 p-2 bg-zinc-900/50 hover:bg-zinc-900 border border-white/5 rounded-lg cursor-grab active:cursor-grabbing transition-colors"
                            >
                                <BrainCircuit
                                    class="w-4 h-4 text-red-400"
                                />
                                <span class="text-xs font-medium text-zinc-300"
                                    >Metrics Visualizer</span
                                >
                            </div>
                        </div>
                    </div>
                </div>
            </aside>
        {/if}

        <!-- Canvas Area -->
        <main
            class="flex-1 relative bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDAiIGhlaWdodD0iNDAiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+PHBhdGggZD0iTTAgMGg0MHY0MEgweiIgZmlsbD0ibm9uZSIvPPHBhdGggZD0iTTAgMTBoNDBNMTAgMHY0MCIgc3Ryb2tlPSJyZ2JhKDI1NSwyNTUsMjU1LDAuMDUpIiBzdHJva2Utd2lkdGg9IjEiLz48L3N2Zz4=')] overflow-hidden flex items-center justify-center cursor-crosshair"
        >
            <div
                class="absolute top-4 left-4 bg-zinc-950 border border-white/10 px-3 py-1.5 rounded-lg shadow-lg flex items-center gap-4 z-10"
            >
                <div class="flex items-center gap-2">
                    <div class="w-2 h-2 rounded-full bg-red-500"></div>
                    <span class="text-xs font-medium text-zinc-400"
                        >Untrained</span
                    >
                </div>
                <div class="w-px h-4 bg-zinc-800"></div>
                <div class="text-xs text-zinc-500 font-mono">Zoom: 100%</div>
            </div>

            <!-- Placeholder content for empty canvas visualization -->
            <div
                class="flex flex-col items-center justify-center opacity-40 select-none pointer-events-none"
            >
                <BrainCircuit class="w-24 h-24 text-zinc-700 mb-6" />
                <h2 class="text-2xl font-bold text-zinc-500 mb-2">
                    Playground Canvas
                </h2>
                <p class="text-zinc-600 text-sm">
                    Drag and drop nodes from the panel to start building.
                </p>
            </div>

            <!-- Example Nodes on Canvas to show layout -->
            <div
                class="absolute top-1/3 left-1/4 bg-zinc-900 border border-red-500/50 rounded-xl p-3 shadow-2xl w-48 cursor-move hidden lg:block"
            >
                <div
                    class="flex items-center gap-2 border-b border-white/10 pb-2 mb-3 cursor-grab"
                >
                    <Database class="w-4 h-4 text-red-400" />
                    <span class="text-xs font-bold text-white">Dataset</span>
                </div>
                <div class="text-[10px] text-zinc-400 font-mono">
                    Shape: (1000, 10)
                </div>
                <!-- Outlet port -->
                <div
                    class="absolute right-0 top-1/2 tranzinc-x-1/2 -tranzinc-y-1/2 w-4 h-4 bg-zinc-950 border-2 border-red-500 rounded-full cursor-crosshair"
                ></div>
            </div>

            <!-- Connection line example -->
            <svg
                class="absolute top-0 left-0 w-full h-full pointer-events-none hidden lg:block"
                style="z-index: 0"
            >
                <path
                    d="M 330 350 C 450 350, 450 350, 560 350"
                    fill="none"
                    stroke="rgba(168, 85, 247, 0.5)"
                    stroke-width="3"
                />
            </svg>

            <div
                class="absolute top-1/3 left-1/2 bg-zinc-900 border border-red-700/50 rounded-xl p-3 shadow-2xl w-48 cursor-move hidden lg:block"
            >
                <!-- Inlet port -->
                <div
                    class="absolute left-0 top-1/2 -tranzinc-x-1/2 -tranzinc-y-1/2 w-4 h-4 bg-zinc-950 border-2 border-red-700 rounded-full"
                ></div>

                <div
                    class="flex items-center justify-between border-b border-white/10 pb-2 mb-3 cursor-grab"
                >
                    <div class="flex items-center gap-2">
                        <Network class="w-4 h-4 text-red-500" />
                        <span class="text-xs font-bold text-white"
                            >Dense Layer</span
                        >
                    </div>
                    <Settings
                        class="w-3 h-3 text-zinc-500 hover:text-white cursor-pointer"
                    />
                </div>
                <div class="space-y-2">
                    <div
                        class="flex justify-between items-center bg-zinc-950/50 px-2 py-1.5 rounded"
                    >
                        <span class="text-[10px] text-zinc-400">Neurons</span>
                        <span
                            class="text-[10px] text-white font-mono bg-zinc-800 px-1 rounded"
                            >64</span
                        >
                    </div>
                    <div
                        class="flex justify-between items-center bg-zinc-950/50 px-2 py-1.5 rounded"
                    >
                        <span class="text-[10px] text-zinc-400"
                            >Activation</span
                        >
                        <span class="text-[10px] text-red-400 font-mono"
                            >ReLU</span
                        >
                    </div>
                </div>
            </div>
        </main>

        <!-- Right Metrics Panel (Closed by default or small) -->
        <aside
            class="w-72 border-l border-white/5 bg-zinc-950/40 hidden xl:flex flex-col"
        >
            <div class="p-4 border-b border-white/5 bg-zinc-950/80">
                <h3
                    class="text-xs font-bold text-white flex items-center gap-2"
                >
                    <BarChart class="w-4 h-4 text-red-400" /> Metrics
                </h3>
            </div>
            <div class="p-4 flex-1 flex flex-col gap-6">
                <!-- Placeholder Chart Area -->
                <div class="space-y-2">
                    <div class="flex justify-between items-center">
                        <span class="text-xs font-medium text-zinc-400"
                            >Loss</span
                        >
                        <span class="text-xs font-mono text-red-400"
                            >--</span
                        >
                    </div>
                    <div
                        class="w-full h-32 bg-zinc-900/80 rounded-xl border border-white/5 flex items-end p-2 gap-1 opacity-50"
                    >
                        <!-- fake chart bars -->
                        {#each [40, 35, 30, 28, 25, 20, 15, 12, 10, 8] as h}
                            <div
                                class="flex-1 bg-red-500/50 rounded-sm"
                                style="height: {h}%"
                            ></div>
                        {/each}
                    </div>
                </div>

                <div class="space-y-2">
                    <div class="flex justify-between items-center">
                        <span class="text-xs font-medium text-zinc-400"
                            >Accuracy</span
                        >
                        <span class="text-xs font-mono text-red-400">--</span>
                    </div>
                    <div
                        class="w-full h-32 bg-zinc-900/80 rounded-xl border border-white/5 flex items-end p-2 gap-1 opacity-50"
                    >
                        <!-- fake chart bars -->
                        {#each [10, 20, 35, 50, 65, 75, 82, 88, 92, 95] as h}
                            <div
                                class="flex-1 bg-red-500/50 rounded-sm"
                                style="height: {h}%"
                            ></div>
                        {/each}
                    </div>
                </div>
            </div>
        </aside>
    </div>
</div>
