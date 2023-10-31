<script>
    import { fade } from "svelte/transition";
    import { pb } from "$lib/pocketbase";

    let modal;
    export let portfolio = [];

    let caricamento = false,
        tipo,
        input,
        file,
        record,
        loadingImage = true;

    export function mostra(post) {
        loadingImage = true;
        record = post;
        tipo = record.tipo;
        console.log("tipo", tipo);
        modal.showModal();
        file = {
            file: post.file,
            url:
                "https://pb_anna.myapollo.it/api/files/portfolio/" +
                post.id +
                "/" +
                post.file +
                "?thumb=500x500f",
        };
    }

    function caricaAnteprima() {
        file = {
            file: input.files[0],
            url: URL.createObjectURL(input.files[0]),
        };
    }

    async function uploadFile() {
        caricamento = true;
        const formData = new FormData();
        if (input.files.length > 0) {
            formData.append("file", input.files[0]);
        }
        formData.append("tipo", tipo);
        try {
            const temp = await pb
                .collection("portfolio")
                .update(record.id, formData);
            portfolio = portfolio.filter((el) => el.id != record.id);
            portfolio = [temp, ...portfolio];
            caricamento = false;
            modal.close();
        } catch (error) {
            console.log("error", error);
        }
    }

    function promptCancella() {
        if (confirm("Sei sicuro di voler cancellare questo post?")) {
            cancellaPost();
        }
    }

    async function cancellaPost() {
        console.log("Ok, cancella il post", record);
        try {
            await pb.collection("portfolio").delete(record.id);
            portfolio = portfolio.filter((el) => el.id != record.id);
            modal.close();
        } catch (error) {
            alert("Errore durante la cancellazione del post");
        }
    }

    function immagineCaricata() {
        loadingImage = false;
    }

    function cambiaTipo() {
        console.log("cambio tipo da", tipo);
        if (tipo === "biglietto") tipo = "tela";
        else tipo = "biglietto";
        console.log("a", tipo);
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
            class="mt-4 h-auto w-full"
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
                    class="w-full max-h-80 relative rounded-lg"
                    transition:fade
                    hidden={loadingImage}
                >
                    <img
                        src={file.url}
                        alt=""
                        class="rounded-lg max-h-80 mx-auto"
                        on:load={immagineCaricata}
                    />
                    <div
                        class="absolute bottom-4 right-4 btn btn-circle z-10 btn-sm"
                    >
                        <svg
                            class="w-4 h-4"
                            viewBox="0 0 24 24"
                            fill="none"
                            xmlns="http://www.w3.org/2000/svg"
                        >
                            <path
                                fill-rule="evenodd"
                                clip-rule="evenodd"
                                d="M20.8477 1.87868C19.6761 0.707109 17.7766 0.707105 16.605 1.87868L2.44744 16.0363C2.02864 16.4551 1.74317 16.9885 1.62702 17.5692L1.03995 20.5046C0.760062 21.904 1.9939 23.1379 3.39334 22.858L6.32868 22.2709C6.90945 22.1548 7.44285 21.8693 7.86165 21.4505L22.0192 7.29289C23.1908 6.12132 23.1908 4.22183 22.0192 3.05025L20.8477 1.87868ZM18.0192 3.29289C18.4098 2.90237 19.0429 2.90237 19.4335 3.29289L20.605 4.46447C20.9956 4.85499 20.9956 5.48815 20.605 5.87868L17.9334 8.55027L15.3477 5.96448L18.0192 3.29289ZM13.9334 7.3787L3.86165 17.4505C3.72205 17.5901 3.6269 17.7679 3.58818 17.9615L3.00111 20.8968L5.93645 20.3097C6.13004 20.271 6.30784 20.1759 6.44744 20.0363L16.5192 9.96448L13.9334 7.3787Z"
                                fill="#0F0F0F"
                            />
                        </svg>
                    </div>
                </div>
                <div class="w-full h-80" transition:fade hidden={!loadingImage}>
                    <div class="w-full h-full flex items-center justify-center">
                        <span
                            class="loading loading-infinity loading-lg mx-auto"
                        />
                    </div>
                </div>
                <input
                    type="file"
                    name="file"
                    id="file"
                    bind:this={input}
                    accept="image/*"
                    class="hidden"
                    on:change={caricaAnteprima}
                />
            {/if}
        </div>

        <div class="mt-4">
            <fieldset class="grid grid-cols-2 gap-4">
                <div>
                    <input
                        type="radio"
                        name="tipoMod"
                        value="tela"
                        id="telaMod"
                        class="peer hidden [&:checked_+_label_svg]:block"
                        bind:group={tipo}
                    />

                    <label
                        for="telaMod"
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
                        name="tipoMod"
                        value="biglietto"
                        id="bigliettoMod"
                        class="peer hidden [&:checked_+_label_svg]:block"
                        bind:group={tipo}
                    />

                    <label
                        for="bigliettoMod"
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
        <div class="mt-4 flex w-full justify-between">
            <button
                class="btn btn-primary"
                disabled={caricamento}
                on:click={uploadFile}
            >
                Aggiorna
            </button>
            <button class="btn btn-error btn-circle" on:click={promptCancella}>
                <svg
                    class="w-6 h-6"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <path
                        d="M4 6H20M16 6L15.7294 5.18807C15.4671 4.40125 15.3359 4.00784 15.0927 3.71698C14.8779 3.46013 14.6021 3.26132 14.2905 3.13878C13.9376 3 13.523 3 12.6936 3H11.3064C10.477 3 10.0624 3 9.70951 3.13878C9.39792 3.26132 9.12208 3.46013 8.90729 3.71698C8.66405 4.00784 8.53292 4.40125 8.27064 5.18807L8 6M18 6V16.2C18 17.8802 18 18.7202 17.673 19.362C17.3854 19.9265 16.9265 20.3854 16.362 20.673C15.7202 21 14.8802 21 13.2 21H10.8C9.11984 21 8.27976 21 7.63803 20.673C7.07354 20.3854 6.6146 19.9265 6.32698 19.362C6 18.7202 6 17.8802 6 16.2V6M14 10V17M10 10V17"
                        stroke="#000000"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    />
                </svg>
            </button>
        </div>
    </div>
    <form method="dialog" class="modal-backdrop">
        <button>close</button>
    </form>
</dialog>
