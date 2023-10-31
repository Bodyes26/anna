<script>
    import { pb, currentUser } from "$lib/pocketbase";
    import { onMount } from "svelte";
    import { goto } from "$app/navigation";
    import { fade } from "svelte/transition";
    import ModalNew from "./modalNew.svelte";
    import ModalModify from "./modalModify.svelte";

    let loading = true,
        portfolio = [],
        modalNew,
        modalModify;
    onMount(async () => {
        console.log("currentUser", $currentUser);
        if ($currentUser == null) goto("/admin/login");
        else if ($currentUser.id == undefined) goto("/admin/login");
        else if ($currentUser.collectionName === "users") goto("/admin/login");
        else {
            let temp = await pb.collection("portfolio").getFullList({
                sort: "-created",
            });

            for (let index = 0; index < temp.length; index++) {
                const element = temp[index];
                element.loading = true;
                portfolio = [...portfolio, element];
            }
            loading = false;
        }
    });

    function modificaPost(post) {
        modalModify.mostra(post);
    }
</script>

{#if loading}
    <div
        class="w-screen h-screen flex justify-center items-center absolute z-10 left-0 top-0 bg-white"
        transition:fade
    >
        <span class="loading loading-spinner loading-lg" />
    </div>
{/if}

<div class="w-screen min-h-screen mt-4 md:mt-8 px-2 md:px-4">
    <h1 class="text-4xl font-bold">Bentornata, Anna!</h1>
    <div class="mt-8 w-full">
        <h2 class="text-2xl font-semibold">Ultimi post</h2>
        <div class="grid mt-2 grid-cols-3 gap-4">
            {#each portfolio as el}
                <div class="flex flex-col">
                    <!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
                    <img
                        src="https://pb_anna.myapollo.it/api/files/portfolio/{el.id}/{el.file}?thumb=200x200f"
                        alt=""
                        hidden={el.loading}
                        on:click={() => modificaPost(el)}
                        on:keypress={(e) => {
                            if (e.key === "Enter") modificaPost(el);
                        }}
                        on:load={() => (el.loading = false)}
                    />
                    <div class="w-full" hidden={!el.loading}>
                        <div
                            class="w-full h-32 border rounded-lg border-black flex items-center justify-center"
                        >
                            <span
                                class="loading loading-infinity loading-lg mx-auto"
                            />
                        </div>
                    </div>
                    <span class="text-lg font-bold">
                        {el.tipo}
                    </span>
                    <span class="text-md italic text-gray-600">
                        {new Date(el.updated).toLocaleDateString("en-GB")}
                    </span>
                </div>
            {/each}
        </div>
    </div>
</div>
<div class="fixed bottom-4 left-0 w-full px-4">
    <button
        class="btn rounded-full w-full btn-success"
        on:click={() => modalNew.showModal()}
    >
        Carica nuovo
    </button>
</div>

{#if !loading}
    <ModalNew bind:modal={modalNew} bind:portfolio />
    <ModalModify bind:this={modalModify} bind:portfolio />
{/if}
