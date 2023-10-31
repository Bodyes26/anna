<script>
    import { slide } from "svelte/transition";
    import { pb } from "$lib/pocketbase";
    export let modal;
    export let portfolio = [];
    let caricamento = false,
        tipo = null,
        input,
        file = null;

    function caricaAnteprima() {
        if (input.files.length > 0) {
            file = input.files[0];
        } else {
            file = null;
        }
    }

    async function uploadFile() {
        if (file == null) {
            alert("Devi caricare un file!");
            return;
        }
        if (tipo == null) {
            alert("Devi scegliere un tipo!");
            return;
        }
        caricamento = true;
        const formData = new FormData();
        formData.append("file", file);
        formData.append("tipo", tipo);
        try {
            const record = await pb.collection("portfolio").create(formData);
            portfolio = [record, ...portfolio];
            caricamento = false;
            modal.close();
        } catch (error) {
            console.log("error", error);
        }
    }
</script>

<dialog bind:this={modal} class="modal">
    <div class="modal-box">
        <form method="dialog">
            <button
                class="btn btn-sm btn-circle btn-ghost absolute right-2 top-2"
            >
                ✕
            </button>
        </form>
        <div
            class="mt-2 h-auto btn w-full border max-h-80 overflow-y-scroll py-6"
            on:click={() => {
                if (!caricamento) input.click();
            }}
            on:keydown={() => {
                if (!caricamento) input.click();
            }}
            role="button"
            tabindex="-1"
        >
            {#if file}
                <div
                    class="w-full max-h-60 p-0 mb-2 relative overflow-hidden rounded-lg"
                    transition:slide
                >
                    <img
                        src={URL.createObjectURL(file)}
                        alt=""
                        class="rounded-lg"
                    />
                </div>
            {:else}
                <h1 class="text-xl font-bold text-center">
                    Premi per caricare foto
                </h1>
            {/if}
            <input
                type="file"
                name="file"
                id="file"
                bind:this={input}
                accept="image/*,video/*"
                class="hidden"
                on:change={caricaAnteprima}
            />
        </div>
        <div class="mt-4">
            <fieldset class="grid grid-cols-2 gap-4">
                <div>
                    <input
                        type="radio"
                        name="tipoNew"
                        value="tela"
                        id="telaNew"
                        class="peer hidden [&:checked_+_label_svg]:block"
                        bind:group={tipo}
                    />

                    <label
                        for="telaNew"
                        class="block cursor-pointer rounded-lg border border-gray-400 p-4 text-sm font-medium shadow-sm hover:border-gray-600 peer-checked:border-blue-500 peer-checked:ring-1 peer-checked:ring-blue-500"
                    >
                        <div class="flex items-center justify-between">
                            <p class="text-gray-700">Tela</p>

                            <svg
                                class="hidden h-5 w-5 text-blue-600"
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 20 20"
                                fill="currentColor"
                            >
                                <path
                                    fill-rule="evenodd"
                                    d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                                    clip-rule="evenodd"
                                />
                            </svg>
                        </div>
                    </label>
                </div>

                <div>
                    <input
                        type="radio"
                        name="tipoNew"
                        value="biglietto"
                        id="bigliettoNew"
                        class="peer hidden [&:checked_+_label_svg]:block"
                        bind:group={tipo}
                    />

                    <label
                        for="bigliettoNew"
                        class="block cursor-pointer rounded-lg border border-gray-400 p-4 text-sm font-medium shadow-sm hover:border-gray-600 peer-checked:border-blue-500 peer-checked:ring-1 peer-checked:ring-blue-500"
                    >
                        <div class="flex items-center justify-between">
                            <p class="text-gray-700">Biglietto</p>

                            <svg
                                class="hidden h-5 w-5 text-blue-600"
                                xmlns="http://www.w3.org/2000/svg"
                                viewBox="0 0 20 20"
                                fill="currentColor"
                            >
                                <path
                                    fill-rule="evenodd"
                                    d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z"
                                    clip-rule="evenodd"
                                />
                            </svg>
                        </div>
                    </label>
                </div>
            </fieldset>
        </div>
        <div class="mt-4">
            <button
                class="btn btn-primary w-full"
                disabled={caricamento}
                on:click={uploadFile}
            >
                Carica
            </button>
        </div>
    </div>
    <form method="dialog" class="modal-backdrop">
        <button>close</button>
    </form>
</dialog>
