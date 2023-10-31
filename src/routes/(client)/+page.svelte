<script>
    import { onMount } from "svelte";
    import { pb } from "$lib/pocketbase";
    import { slide } from "svelte/transition";
    import { page } from "$app/stores";
    import { Fancybox } from "@fancyapps/ui";
    import { MetaTags } from "svelte-meta-tags";

    import "@fancyapps/ui/dist/fancybox/fancybox.css";
    let images = [],
        showToastRingrazia,
        websiteTitle =
            "Anna.rt | Arte su Tela e Biglietti di Auguri Fatti a Mano",
        websiteDescription =
            "Opere d'arte su tela e biglietti di auguri unici realizzati a mano. Scopri disegni straordinari che catturano emozioni e storie.";

    onMount(async () => {
        const records = await pb.collection("portfolio").getFullList({
            sort: "-created",
        });
        images = records;
        let thanks = $page.url.search.slice(1).split("=")[1];
        if (thanks === "1") {
            showToastRingrazia = true;
            setTimeout(() => {
                showToastRingrazia = false;
            }, 3000);
        }
        const options = {
            Toolbar: {
                display: {
                    left: ["infobar"],
                    middle: [],
                    right: ["download", "close"],
                },
            },
        };
        Fancybox.bind("[data-fancybox]", options);
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
<img
    src="/images/homepage.png"
    alt="Anna's Art logo"
    class="w-full md:w-3/5 mx-auto"
/>
<div>
    <div class="quote-wrapper">
        <div class="quote">
            Paintings have a life of their own that derives from the painter's
            soul.
        </div>
        <div class="quote-author">~ Vincent Van Gogh</div>
    </div>
    <h1 class="text-center text-3xl font-bold mt-8">Ultimi lavori</h1>
    <div class="grid grid-cols-1 gap-2 md:grid-cols-3 mt-4 lg:mt-8 mx-4">
        {#each images as image, i}
            {#if i < 6}
                <a
                    href="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}"
                    data-fancybox="gallery"
                    data-download-src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?download=1"
                >
                    <img
                        src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=500x500f"
                        class="aspect-square object-cover"
                        alt=""
                    />
                </a>
            {/if}
        {/each}
    </div>
</div>

{#if showToastRingrazia}
    <div class="toast toast-center" transition:slide>
        <div class="alert alert-success">
            <span>Messaggio inviato, grazie!</span>
        </div>
    </div>
{/if}

<style>
    @font-face {
        font-family: "Paragon";
        src: url("/fonts/Paragon_italic.otf");
    }

    .quote-wrapper {
        margin: 0 auto;
        width: 100%;
        max-width: 600px;
        padding: 0 20px;
        font-family: "Paragon", serif;
    }

    .quote {
        width: 100%;
        font-size: 1.2rem;
        text-align: justify;
    }

    .quote-author {
        width: 100%;
        font-size: 1rem;
        text-align: right;
        margin-top: 8px;
    }
</style>
