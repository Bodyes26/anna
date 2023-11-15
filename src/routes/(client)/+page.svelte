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
        for (let index = 0; index < images.length; index++) {
            images[index].loading = true;
        }
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
    class="w-full md:w-3/5 mx-auto mt-12"
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
    <div class="grid gap-2 grid-cols-3 mt-4 lg:mt-8 mx-4">
        {#if images.length === 0}
            <div class="col-span-3">
                <div class="w-full h-40 flex items-center justify-center">
                    <span class="loading loading-infinity loading-lg mx-auto" />
                </div>
            </div>
        {/if}
        {#each images as image, i}
            {#if i < 6}
                <a
                    href="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}"
                    data-fancybox="gallery"
                    data-download-src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?download=1"
                >
                    <div class="relative">
                        <img
                            src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=500x500f"
                            class={image.loading
                                ? "opacity-0 z-10 absolute inset-0 transition-all duration-500 ease-in-out"
                                : "aspect-square object-cover opacity-100 transition-all duration-500 ease-in-out"}
                            alt=""
                            on:load={() => {
                                image.loading = false;
                            }}
                        />
                        <div class={image.loading ? "block" : "hidden"}>
                            <div
                                class="w-full h-32 border rounded-lg border-black flex items-center justify-center"
                            >
                                <span
                                    class="loading loading-infinity loading-lg mx-auto"
                                />
                            </div>
                        </div>
                    </div>
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
