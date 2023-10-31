<script>
    import { slide } from "svelte/transition";
    import { goto } from "$app/navigation";
    import { pb } from "$lib/pocketbase";
    let loading = false,
        username,
        password,
        showToastError = false;

    async function effettuaLogin() {
        loading = true;
        try {
            await pb.admins.authWithPassword(username, password);
            goto("/admin");
        } catch (error) {
            showToastError = true;
            setTimeout(() => {
                showToastError = false;
            }, 3000);
        } finally {
            loading = false;
        }
    }
</script>

<form
    on:submit|preventDefault={effettuaLogin}
    class="w-screen min-h-screen flex flex-col justify-center items-center"
>
    <h1 class="text-4xl font-semibold text-center">ADMIN</h1>
    <div class="w-full max-w-xs md:max-w-md lg:max-w-lg mt-4">
        <label for="username" class="label">
            <span class="label-text">Email</span>
        </label>
        <input
            type="email"
            placeholder="admin@example.com"
            class="input input-bordered w-full"
            required
            autocomplete="username"
            bind:value={username}
        />
    </div>
    <div class="w-full max-w-xs md:max-w-md lg:max-w-lg mt-4">
        <label for="password" class="label">
            <span class="label-text">Password</span>
        </label>
        <input
            type="password"
            placeholder="•••••••••"
            class="input input-bordered w-full"
            required
            autocomplete="current-password"
            bind:value={password}
        />
    </div>
    <div
        class="w-full max-w-xs md:max-w-md lg:max-w-lg mt-4 grid grid-cols-2 gap-2"
    >
        <button type="submit" class="btn btn-primary w-full">login</button>
        <button type="reset" class="btn w-full">cancella</button>
    </div>
</form>

{#if showToastError}
    <div class="toast toast-center" transition:slide>
        <div class="alert alert-error">
            <span>Errore nel login!</span>
        </div>
    </div>
{/if}
