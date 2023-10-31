<script>
    import { pb } from "$lib/pocketbase";
    import { onMount } from "svelte";
    import ModalBiglietti from "./modalBiglietti.svelte";
    import ModalTele from "./modalTele.svelte";
    import { MetaTags } from "svelte-meta-tags";

    let tele = [],
        biglietti = [],
        modalTele,
        modalBiglietti,
        websiteTitle = "Anna.rt | Ordina tele e biglietti fatti a mano",
        websiteDescription =
            "Opere d'arte su tela e biglietti di auguri unici realizzati a mano. Scopri disegni straordinari che catturano emozioni e storie.";

    onMount(async () => {
        let filterTele = "tipo = 'tela'";
        let filterBiglietti = "tipo = 'biglietto'";
        const temp1 = await pb.collection("portfolio").getList(1, 3, {
            filter: filterTele,
        });
        tele = temp1.items;
        const temp2 = await pb.collection("portfolio").getList(1, 3, {
            filter: filterBiglietti,
        });
        biglietti = temp2.items;
    });
</script>

<MetaTags
    title={websiteTitle}
    description={websiteDescription}
    canonical="https://annartworks.it"
    openGraph={{
        url: "https://annartworks.it",
        title: websiteTitle,
        description: websiteDescription,
        images: [
            {
                url: "https://annartworks.it/images/homepage.png",
                width: 800,
                height: 600,
                alt: "Anna.rt logo",
            },
        ],
        site_name: websiteTitle,
    }}
    twitter={{
        site: "@annartworks.it",
        cardType: "summary_large_image",
        title: websiteTitle,
        description: websiteDescription,
        image: "https://annartworks.it/images/homepage.png",
        imageAlt: "Anna.rt logo",
    }}
/>
<div
    class="grid grid-cols-1 md:grid-cols-2 gap-2 md:gap-4 mt-8 mx-4 lg:mx-8 justify-items-center justify-center"
>
    <div class="card">
        <h1 class="text-4xl font-medium font-serif my-2">Tele</h1>
        <p>
            Vuoi fare un regalo personalizzato? Scegli la dimensione della tela
            e aggiungi una breve descrizione. Ti ricontatterò per avere maggiori
            informazioni.
        </p>
        <div class="flex gap-2 mt-4">
            {#each tele as image}
                <img
                    src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=200x200f"
                    class="aspect-square object-cover w-1/4"
                    alt=""
                />
            {/each}
        </div>
        <div class="w-full flex justify-center mt-4">
            <button
                on:click={() => modalTele.showModal()}
                class="btn btn-primary px-12"
            >
                Prenota una tela
            </button>
        </div>
    </div>
    <div class="card">
        <h1 class="text-4xl font-medium font-serif my-2">Biglietti</h1>
        <p class="">
            Hai bisogno di un biglietto personalizzato? Seleziona l’occasione
            per cui ti serve e aggiungi una breve descrizione. Ti ricontatterò
            per avere maggiori informazioni.
        </p>
        <div class="flex gap-2 mt-4">
            {#each biglietti as image}
                <img
                    src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=200x200f"
                    class="aspect-square object-cover w-1/4"
                    alt=""
                />
            {/each}
        </div>
        <div class="w-full flex justify-center mt-4">
            <button
                on:click={() => modalBiglietti.showModal()}
                class="btn btn-primary px-12">Prenota un biglietto</button
            >
        </div>
    </div>
</div>

<ModalBiglietti bind:modal={modalBiglietti} />
<ModalTele bind:modal={modalTele} />
