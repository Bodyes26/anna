<script>
    import { onMount } from "svelte";
    import { pb } from "$lib/pocketbase";
    import { Fancybox } from "@fancyapps/ui";
    import { MetaTags } from "svelte-meta-tags";
    import "@fancyapps/ui/dist/fancybox/fancybox.css";
    let images = [],
        websiteTitle = "Anna.rt | Portfolio di tele e biglietti fatti a mano",
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

        const options = {
            Toolbar: {
                display: {
                    left: ["infobar"],
                    middle: [],
                    right: ["close"],
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

<h1 class="text-center font-medium text-4xl mt-8">Portfolio</h1>
<div class="grid grid-cols-3 gap-1 mt-4 lg:mt-8 mx-4">
    {#if images.length === 0}
        <div class="col-span-3">
            <div class="w-full h-40 flex items-center justify-center">
                <span class="loading loading-infinity loading-lg mx-auto" />
            </div>
        </div>
    {/if}
    {#each images as image}
        <a
            href="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}"
            data-fancybox="gallery"
            data-download-src="/api/download?{image.id}/{image.file}"
        >
            <div class="relative">
                <img
                    src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=200x200f"
                    class={image.loading
                        ? "opacity-0 z-10 absolute inset-0 transition-all duration-500 ease-in-out"
                        : "aspect-square object-cover opacity-100 transition-all duration-500 ease-in-out  "}
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
    {/each}
</div>
