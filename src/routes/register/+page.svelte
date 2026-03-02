<script>
    import { goto } from "$app/navigation";
    import AuthCard from "../../components/AuthCard.svelte";
    import { login as storeLogin } from "../../stores/auth";
    import { User } from "lucide-svelte";

    let name = "";
    let email = "";
    let password = "";
    let role = "student";
    let isSubmitting = false;

    const handleRegister = (e) => {
        e.preventDefault();
        isSubmitting = true;

        setTimeout(() => {
            storeLogin(email, role);
            goto("/playground");
            isSubmitting = false;
        }, 1000);
    };
</script>

<AuthCard
    title="Create an account"
    subtitle="Join the AI Sandbox to start learning."
>
    <form onsubmit={handleRegister} class="space-y-4">
        <div class="grid grid-cols-2 gap-3 mb-6">
            <!-- svelte-ignore a11y_click_events_have_key_events -->
            <!-- svelte-ignore a11y_no_static_element_interactions -->
            <div
                onclick={() => (role = "student")}
                class="cursor-pointer border {role === 'student'
                    ? 'border-blue-500 bg-blue-500/10'
                    : 'border-slate-700 bg-slate-900 hover:bg-slate-800'} rounded-xl p-3 flex flex-col items-center gap-2 transition-all"
            >
                <User
                    class="w-6 h-6 {role === 'student'
                        ? 'text-blue-400'
                        : 'text-slate-400'}"
                />
                <span
                    class="text-sm font-semibold {role === 'student'
                        ? 'text-blue-400'
                        : 'text-slate-400'}">Student</span
                >
            </div>
            <!-- svelte-ignore a11y_click_events_have_key_events -->
            <!-- svelte-ignore a11y_no_static_element_interactions -->
            <div
                onclick={() => (role = "teacher")}
                class="cursor-pointer border {role === 'teacher'
                    ? 'border-blue-500 bg-blue-500/10'
                    : 'border-slate-700 bg-slate-900 hover:bg-slate-800'} rounded-xl p-3 flex flex-col items-center gap-2 transition-all"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    class={role === "teacher"
                        ? "text-blue-400"
                        : "text-slate-400"}
                    ><path d="M22 10v6M2 10l10-5 10 5-10 5z" /><path
                        d="M6 12v5c3 3 9 3 12 0v-5"
                    /></svg
                >
                <span
                    class="text-sm font-semibold {role === 'teacher'
                        ? 'text-blue-400'
                        : 'text-slate-400'}">Educator</span
                >
            </div>
        </div>

        <div>
            <label
                for="name"
                class="block text-sm font-medium text-slate-300 mb-1.5"
                >Full Name</label
            >
            <input
                type="text"
                id="name"
                bind:value={name}
                required
                class="w-full bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-colors"
                placeholder="John Doe"
            />
        </div>

        <div>
            <label
                for="email"
                class="block text-sm font-medium text-slate-300 mb-1.5"
                >Email address</label
            >
            <input
                type="email"
                id="email"
                bind:value={email}
                required
                class="w-full bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-colors"
                placeholder="you@example.com"
            />
        </div>

        <div>
            <label
                for="password"
                class="block text-sm font-medium text-slate-300 mb-1.5"
                >Password</label
            >
            <input
                type="password"
                id="password"
                bind:value={password}
                required
                class="w-full bg-slate-900 border border-slate-700 rounded-xl px-4 py-3 text-white placeholder-slate-500 focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500 transition-colors"
                placeholder="••••••••"
            />
        </div>

        <button
            type="submit"
            disabled={isSubmitting}
            class="w-full {role === 'teacher'
                ? 'bg-blue-600 hover:bg-blue-500 shadow-[0_0_15px_rgba(239,68,68,0.3)]'
                : 'bg-blue-600 hover:bg-blue-500 shadow-[0_0_15px_rgba(37,99,235,0.3)]'} disabled:opacity-50 text-white font-bold py-3 rounded-xl transition-colors mt-6"
        >
            {isSubmitting ? "Creating account..." : "Create Account"}
        </button>

        <p class="text-center text-sm text-slate-400 mt-6">
            Already have an account? <a
                href="/login"
                class="text-blue-400 hover:text-blue-300 font-semibold"
                >Log in</a
            >
        </p>
    </form>
</AuthCard>
