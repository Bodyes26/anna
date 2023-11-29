<script>
    import { pb } from "$lib/pocketbase";
    import { page } from "$app/stores";
    import { MetaTags } from "svelte-meta-tags";

    let loading = false,
        nome,
        mail,
        messaggio,
        websiteTitle = "Anna.rt | Contatti",
        websiteDescription =
            "Opere d'arte su tela e biglietti di auguri unici realizzati a mano. Scopri disegni straordinari che catturano emozioni e storie.";

    async function salvaMessaggio() {
        loading = true;
        const data = {
            nome: nome,
            email: mail,
            messaggio: messaggio,
        };
        try {
            await pb.collection("messaggi").create(data);
            return true;
        } catch (error) {
            return false;
        }
    }
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
    class="grid grid-cols-1 md:grid-cols-2 gap-4 justify-items-center items-center mt-16 w-full"
>
    <div class="w-full flex flex-col gap-4 items-center justify-center">
        <h1 class="text-6xl font-serif font-medium">Contattami</h1>
        <div class="flex gap-2">
            <a class="Btn" href="https://www.instagram.com/_anna.rt/">
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    height="1.5em"
                    viewBox="0 0 448 512"
                    class="svgIcon"
                    ><path
                        d="M224.1 141c-63.6 0-114.9 51.3-114.9 114.9s51.3 114.9 114.9 114.9S339 319.5 339 255.9 287.7 141 224.1 141zm0 189.6c-41.1 0-74.7-33.5-74.7-74.7s33.5-74.7 74.7-74.7 74.7 33.5 74.7 74.7-33.6 74.7-74.7 74.7zm146.4-194.3c0 14.9-12 26.8-26.8 26.8-14.9 0-26.8-12-26.8-26.8s12-26.8 26.8-26.8 26.8 12 26.8 26.8zm76.1 27.2c-1.7-35.9-9.9-67.7-36.2-93.9-26.2-26.2-58-34.4-93.9-36.2-37-2.1-147.9-2.1-184.9 0-35.8 1.7-67.6 9.9-93.9 36.1s-34.4 58-36.2 93.9c-2.1 37-2.1 147.9 0 184.9 1.7 35.9 9.9 67.7 36.2 93.9s58 34.4 93.9 36.2c37 2.1 147.9 2.1 184.9 0 35.9-1.7 67.7-9.9 93.9-36.2 26.2-26.2 34.4-58 36.2-93.9 2.1-37 2.1-147.8 0-184.8zM398.8 388c-7.8 19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5 9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7 9-132.1c7.8-19.6 22.9-34.7 42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6 132.1 9c19.6 7.8 34.7 22.9 42.6 42.6 11.7 29.5 9 99.5 9 132.1s2.7 102.7-9 132.1z"
                        fill="#FFFFFF"
                    />
                </svg>
                <span class="text">Instagram</span>
            </a>
            <a class="Btn" href="mailto:nanna.migliore@gmail.com">
                <svg
                    height="1.5em"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    class="svgIcon"
                >
                    <path
                        d="M10 19H6.2C5.0799 19 4.51984 19 4.09202 18.782C3.71569 18.5903 3.40973 18.2843 3.21799 17.908C3 17.4802 3 16.9201 3 15.8V8.2C3 7.0799 3 6.51984 3.21799 6.09202C3.40973 5.71569 3.71569 5.40973 4.09202 5.21799C4.51984 5 5.0799 5 6.2 5H17.8C18.9201 5 19.4802 5 19.908 5.21799C20.2843 5.40973 20.5903 5.71569 20.782 6.09202C21 6.51984 21 7.0799 21 8.2V10M20.6067 8.26229L15.5499 11.6335C14.2669 12.4888 13.6254 12.9165 12.932 13.0827C12.3192 13.2295 11.6804 13.2295 11.0677 13.0827C10.3743 12.9165 9.73279 12.4888 8.44975 11.6335L3.14746 8.09863M14 21L16.025 20.595C16.2015 20.5597 16.2898 20.542 16.3721 20.5097C16.4452 20.4811 16.5147 20.4439 16.579 20.399C16.6516 20.3484 16.7152 20.2848 16.8426 20.1574L21 16C21.5523 15.4477 21.5523 14.5523 21 14C20.4477 13.4477 19.5523 13.4477 19 14L14.8426 18.1574C14.7152 18.2848 14.6516 18.3484 14.601 18.421C14.5561 18.4853 14.5189 18.5548 14.4903 18.6279C14.458 18.7102 14.4403 18.7985 14.405 18.975L14 21Z"
                        stroke="#FFFFFF"
                        stroke-width="2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                    />
                </svg>
                <span class="text">Email</span>
            </a>
        </div>
    </div>

    <div class="w-full">
        <form
            action="https://formsubmit.co/5f02f38c408f6b38a132b44e9174296f"
            method="POST"
            class="px-8"
            on:submit={salvaMessaggio}
        >
            <label for="nome" class="label">
                <span class="label-text">Nome</span>
            </label>
            <input
                type="text"
                name="nome"
                class="input input-bordered w-full"
                placeholder="Il tuo nome"
                bind:value={nome}
            />
            <label for="email" class="label">
                <span class="label-text">Email</span>
            </label>
            <input
                type="email"
                name="email"
                class="input input-bordered w-full"
                placeholder="annart@example.com"
                bind:value={mail}
            />

            <label for="richiesta" class="label">
                <span class="label-text">Messaggio</span>
            </label>
            <textarea
                name="richiesta"
                class="textarea textarea-bordered w-full"
                rows="3"
                placeholder="Il tuo messaggio"
                bind:value={messaggio}
            />
            <input
                type="hidden"
                name="_subject"
                value="Messaggio da annartworks.it"
            />
            <input type="hidden" name="_captcha" value="false" />
            <input
                type="hidden"
                name="_next"
                value="{$page.url.origin}/?thanks=1"
            />
            <div class="w-full flex justify-center">
                <button type="submit" class="button mt-4" disabled={loading}>
                    Invia
                    {#if loading}
                        <span class="loading loading-infinity loading-sm" />
                    {/if}
                </button>
            </div>
        </form>
    </div>
</div>

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
        box-shadow:
            inset 0 0 0 4px #ef476f,
            inset 0 0 0 8px #ffd166,
            inset 0 0 0 12px #06d6a0,
            inset 0 0 0 16px #118ab2;
        background: #073b4c;
        color: #fff;
    }

    .Btn {
        border: none;
        border-radius: 50%;
        width: 45px;
        height: 45px;
        display: flex;
        align-items: center;
        justify-content: center;
        transition-duration: 0.4s;
        cursor: pointer;
        position: relative;
        background: #f09433;
        background: -moz-linear-gradient(
            45deg,
            #f09433 0%,
            #e6683c 25%,
            #dc2743 50%,
            #cc2366 75%,
            #bc1888 100%
        );
        background: -webkit-linear-gradient(
            45deg,
            #f09433 0%,
            #e6683c 25%,
            #dc2743 50%,
            #cc2366 75%,
            #bc1888 100%
        );
        background: linear-gradient(
            45deg,
            #f09433 0%,
            #e6683c 25%,
            #dc2743 50%,
            #cc2366 75%,
            #bc1888 100%
        );
        overflow: hidden;
    }

    .svgIcon {
        transition-duration: 0.3s;
    }

    .text {
        position: absolute;
        color: rgb(255, 255, 255);
        width: 120px;
        font-weight: 600;
        opacity: 0;
        transition-duration: 0.4s;
        text-align: center;
    }

    .Btn:hover {
        width: 110px;
        transition-duration: 0.4s;
        border-radius: 30px;
    }

    .Btn:hover .text {
        opacity: 1;
        transition-duration: 0.4s;
    }

    .Btn:hover .svgIcon {
        opacity: 0;
        transition-duration: 0.3s;
    }
</style>
