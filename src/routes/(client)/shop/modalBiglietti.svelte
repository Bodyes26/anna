<script>
    import { page } from "$app/stores";
    export let modal;

    let select,
        showAltro = false,
        loading = false;

    function checkAltro() {
        if (select.value === "Altro") {
            showAltro = true;
        } else {
            showAltro = false;
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
        <form
            action="https://formsubmit.co/5f02f38c408f6b38a132b44e9174296f"
            method="POST"
            class="grid justify-items-center justify-center"
            on:submit={() => (loading = true)}
        >
            <input
                type="hidden"
                name="_subject"
                value="Richiesta biglietto da annartworks.it"
            />
            <input type="hidden" name="_captcha" value="false" />
            <input
                type="hidden"
                name="_next"
                value="{$page.url.origin}/?thanks=1"
            />

            <div class="form-control w-full max-w-xs md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Nome</span>
                </label>
                <input
                    type="text"
                    placeholder="Il tuo nome"
                    name="nome"
                    required
                    class="input input-bordered w-full max-w-xs md:max-w-md lg:max-w-lg"
                />
            </div>
            <div class="form-control w-full max-w-xs md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Indirizzo Email</span>
                </label>
                <input
                    type="email"
                    placeholder="example@gmail.com"
                    name="email"
                    required
                    class="input input-bordered w-full max-w-xs md:max-w-md lg:max-w-lg"
                />
            </div>
            <div class="form-controll w-full max-w-xs md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Occasione del biglietto</span>
                </label>
                <select
                    class="select select-bordered"
                    name="occasione biglietto"
                    bind:this={select}
                    on:change={checkAltro}
                >
                    <option disabled selected>Scegli</option>
                    <option>Compleanno</option>
                    <option>Laurea</option>
                    <option>Anniversario</option>
                    <option>Natale</option>
                    <option>Battesimo</option>
                    <option>Altro</option>
                </select>
            </div>

            {#if showAltro}
                <div
                    class="form-control w-full max-w-xs md:max-w-md lg:max-w-lg"
                >
                    <label for="" class="label">
                        <span class="label-text">Altra occasione</span>
                    </label>
                    <input
                        type="text"
                        placeholder="Per quale occasione?"
                        name="occasione biglietto"
                        class="input input-bordered w-full max-w-xs md:max-w-md lg:max-w-lg"
                    />
                </div>
            {/if}
            <div class="form-control w-full max-w-xs md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text"
                        >Quali idee hai per il biglietto?</span
                    >
                </label>
                <textarea
                    name="richiesta"
                    class="textarea textarea-bordered w-full max-w-xs md:max-w-md lg:max-w-lg"
                    rows="3"
                />
                <label for="" class="label">
                    <span class="label-text-alt">
                        Scrivi quanto vuoi, più dettagli ci sono meglio è!
                    </span>
                </label>
            </div>
            <button type="submit" class="button" disabled={loading}>
                Invia
                {#if loading}
                    <span class="loading loading-infinity loading-sm" />
                {/if}
            </button>
        </form>
    </div>
    <form method="dialog" class="modal-backdrop">
        <button>close</button>
    </form>
</dialog>

<style>
    .button {
        width: 170px;
        height: 60px;
        font-size: 18px;
        background: #fff;
        border: 1px solid gray;
        border-radius: 50px;
        color: #000;
        outline: none;
        cursor: pointer;
        transition: all 0.4s;
        display: flex;
        gap: 0.5rem;
        justify-content: center;
        align-items: center;
    }

    .button:hover {
        box-shadow: inset 0 0 0 4px #ef476f, inset 0 0 0 8px #ffd166,
            inset 0 0 0 12px #06d6a0, inset 0 0 0 16px #118ab2;
        background: #073b4c;
        color: #fff;
    }
</style>
