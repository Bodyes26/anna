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

        console.log(images);
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
<div class="grid grid-cols-1 gap-1 md:grid-cols-3 mt-4 lg:mt-8 mx-4">
    {#each images as image}
        <a
            href="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}"
            data-fancybox="gallery"
            data-download-src="/api/download?{image.id}/{image.file}"
        >
            <img
                src="https://pb_anna.myapollo.it/api/files/portfolio/{image.id}/{image.file}?thumb=200x200"
                class="aspect-square object-cover"
                alt=""
            />
        </a>
    {/each}
</div>
