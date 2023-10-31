<script>
    import { page } from "$app/stores";
    export let modal;

    let loading = false;
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
                value="Richiesta tela da annartworks.it"
            />
            <input type="hidden" name="_captcha" value="false" />
            <input
                type="hidden"
                name="_next"
                value="{$page.url.origin}/?thanks=1"
            />

            <div class="form-control w-full max-w-sm md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Nome</span>
                </label>
                <input
                    type="text"
                    placeholder="Il tuo nome"
                    name="nome"
                    required
                    class="input input-bordered w-full max-w-sm md:max-w-md lg:max-w-lg"
                />
            </div>
            <div class="form-control w-full max-w-sm md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Indirizzo Email</span>
                </label>
                <input
                    type="text"
                    placeholder="example@gmail.com"
                    name="email"
                    required
                    class="input input-bordered w-full max-w-sm md:max-w-md lg:max-w-lg"
                />
            </div>
            <div class="form-controll w-full max-w-sm md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Dimensioni tela</span>
                </label>
                <div class="radio-inputs">
                    <label class="tooltip" data-tip="10x30">
                        <input
                            class="radio-input"
                            type="radio"
                            name="dimensioni"
                            value="piccola"
                        />
                        <span class="radio-tile">
                            <span class="radio-icon">
                                <svg
                                    version="1.1"
                                    id="_x32_"
                                    width="1.2rem"
                                    height="1.2rem"
                                    xmlns="http://www.w3.org/2000/svg"
                                    xmlns:xlink="http://www.w3.org/1999/xlink"
                                    viewBox="0 0 512 512"
                                    xml:space="preserve"
                                >
                                    <style type="text/css">
                                        .st0 {
                                            fill: #000000;
                                        }
                                    </style>
                                    <g>
                                        <path
                                            class="st0"
                                            d="M42.436,0v512H61.6h407.964V0H42.436z M431.228,473.664H80.769V38.328h350.459V473.664z"
                                        />
                                        <path
                                            class="st0"
                                            d="M414.799,450.398V54.757H97.193v402.486h317.606V450.398z M401.11,366.201
		c-3.654-7.718-8.44-14.709-14.695-20.284c-50.18-44.764-45.007-74.203-45.992-92.435c-1.262-23.412,24.05-142.4-89.869-137.962
		c-3.474,4.522-6.993,20.596-6.678,29.14c42.746-1.304,50.313,35.603,50.313,70.728s-17.05,58.344-17.05,58.344
		c-0.804,2.371-2.074,1.733-0.683,3.814c0,0,2.458,2.961,5.458,6.179c3.266,14.237,15.277,32.42,43.634,35.569
		c20.361,2.268,22.392,4.528,31.817,9.404c2.545,2.316,4.404,4.591,5.319,6.782c-20.888-0.957-56.158,26.574-56.158,26.574
		s-34.872,6.768-67.011,5.548c2.559-3.676,5.52-6.858,8.852-9.07c1.523-1.013,1.935-3.079,0.916-4.605
		c-1.016-1.525-3.079-1.942-4.604-0.929c-4.788,3.203-8.61,7.642-11.716,12.441c-0.364,0.569-0.7,1.144-1.048,1.72
		c-18.717-1.539-35.402-6.311-42.146-17.448c-9.889-16.311,52.212-45.562,52.212-45.562v-29.425c0,0-11.674,0.27-26.862-16.179
		c-22.326-24.196-16.876-79.613-7.316-94.897c14.276-22.816,29.428-16.138,29.112-19.93c-1.05-12.65,5.829-28.253,5.829-28.253
		c-4.58,0.222-15.08,2.04-26.002,6.567c-11.751,4.882-30.735,17.539-40.229,68.163c-8.749,46.658,9.455,102.566-1.932,115.853
		c-11.394,13.287-15.191,23.731-15.191,32.276c0,16.387-3.162,32.039-5.062,33.939c-1.769,1.776-18.832,27.573-21.103,71.29h-22.337
		V68.447H401.11V366.201z"
                                        />
                                    </g>
                                </svg>
                            </span>
                            <span class="radio-label">Piccola</span>
                        </span>
                    </label>
                    <label class="tooltip" data-tip="20x40">
                        <input
                            class="radio-input"
                            type="radio"
                            name="dimensioni"
                            value="media"
                        />
                        <span class="radio-tile">
                            <span class="radio-icon">
                                <svg
                                    version="1.1"
                                    id="_x32_"
                                    width="1.5rem"
                                    height="1.5rem"
                                    xmlns="http://www.w3.org/2000/svg"
                                    xmlns:xlink="http://www.w3.org/1999/xlink"
                                    viewBox="0 0 512 512"
                                    xml:space="preserve"
                                >
                                    <style type="text/css">
                                        .st0 {
                                            fill: #000000;
                                        }
                                    </style>
                                    <g>
                                        <path
                                            class="st0"
                                            d="M42.436,0v512H61.6h407.964V0H42.436z M431.228,473.664H80.769V38.328h350.459V473.664z"
                                        />
                                        <path
                                            class="st0"
                                            d="M414.799,450.398V54.757H97.193v402.486h317.606V450.398z M401.11,366.201
		c-3.654-7.718-8.44-14.709-14.695-20.284c-50.18-44.764-45.007-74.203-45.992-92.435c-1.262-23.412,24.05-142.4-89.869-137.962
		c-3.474,4.522-6.993,20.596-6.678,29.14c42.746-1.304,50.313,35.603,50.313,70.728s-17.05,58.344-17.05,58.344
		c-0.804,2.371-2.074,1.733-0.683,3.814c0,0,2.458,2.961,5.458,6.179c3.266,14.237,15.277,32.42,43.634,35.569
		c20.361,2.268,22.392,4.528,31.817,9.404c2.545,2.316,4.404,4.591,5.319,6.782c-20.888-0.957-56.158,26.574-56.158,26.574
		s-34.872,6.768-67.011,5.548c2.559-3.676,5.52-6.858,8.852-9.07c1.523-1.013,1.935-3.079,0.916-4.605
		c-1.016-1.525-3.079-1.942-4.604-0.929c-4.788,3.203-8.61,7.642-11.716,12.441c-0.364,0.569-0.7,1.144-1.048,1.72
		c-18.717-1.539-35.402-6.311-42.146-17.448c-9.889-16.311,52.212-45.562,52.212-45.562v-29.425c0,0-11.674,0.27-26.862-16.179
		c-22.326-24.196-16.876-79.613-7.316-94.897c14.276-22.816,29.428-16.138,29.112-19.93c-1.05-12.65,5.829-28.253,5.829-28.253
		c-4.58,0.222-15.08,2.04-26.002,6.567c-11.751,4.882-30.735,17.539-40.229,68.163c-8.749,46.658,9.455,102.566-1.932,115.853
		c-11.394,13.287-15.191,23.731-15.191,32.276c0,16.387-3.162,32.039-5.062,33.939c-1.769,1.776-18.832,27.573-21.103,71.29h-22.337
		V68.447H401.11V366.201z"
                                        />
                                    </g>
                                </svg>
                            </span>
                            <span class="radio-label">Media</span>
                        </span>
                    </label>
                    <label class="tooltip" data-tip="40x70">
                        <input
                            class="radio-input"
                            type="radio"
                            name="dimensioni"
                            value="grande"
                        />
                        <span class="radio-tile">
                            <span class="radio-icon">
                                <svg
                                    width="2rem"
                                    height="2rem"
                                    version="1.1"
                                    id="_x32_"
                                    xmlns="http://www.w3.org/2000/svg"
                                    xmlns:xlink="http://www.w3.org/1999/xlink"
                                    viewBox="0 0 512 512"
                                    xml:space="preserve"
                                >
                                    <style type="text/css">
                                        .st0 {
                                            fill: #000000;
                                        }
                                    </style>
                                    <g>
                                        <path
                                            class="st0"
                                            d="M42.436,0v512H61.6h407.964V0H42.436z M431.228,473.664H80.769V38.328h350.459V473.664z"
                                        />
                                        <path
                                            class="st0"
                                            d="M414.799,450.398V54.757H97.193v402.486h317.606V450.398z M401.11,366.201
		c-3.654-7.718-8.44-14.709-14.695-20.284c-50.18-44.764-45.007-74.203-45.992-92.435c-1.262-23.412,24.05-142.4-89.869-137.962
		c-3.474,4.522-6.993,20.596-6.678,29.14c42.746-1.304,50.313,35.603,50.313,70.728s-17.05,58.344-17.05,58.344
		c-0.804,2.371-2.074,1.733-0.683,3.814c0,0,2.458,2.961,5.458,6.179c3.266,14.237,15.277,32.42,43.634,35.569
		c20.361,2.268,22.392,4.528,31.817,9.404c2.545,2.316,4.404,4.591,5.319,6.782c-20.888-0.957-56.158,26.574-56.158,26.574
		s-34.872,6.768-67.011,5.548c2.559-3.676,5.52-6.858,8.852-9.07c1.523-1.013,1.935-3.079,0.916-4.605
		c-1.016-1.525-3.079-1.942-4.604-0.929c-4.788,3.203-8.61,7.642-11.716,12.441c-0.364,0.569-0.7,1.144-1.048,1.72
		c-18.717-1.539-35.402-6.311-42.146-17.448c-9.889-16.311,52.212-45.562,52.212-45.562v-29.425c0,0-11.674,0.27-26.862-16.179
		c-22.326-24.196-16.876-79.613-7.316-94.897c14.276-22.816,29.428-16.138,29.112-19.93c-1.05-12.65,5.829-28.253,5.829-28.253
		c-4.58,0.222-15.08,2.04-26.002,6.567c-11.751,4.882-30.735,17.539-40.229,68.163c-8.749,46.658,9.455,102.566-1.932,115.853
		c-11.394,13.287-15.191,23.731-15.191,32.276c0,16.387-3.162,32.039-5.062,33.939c-1.769,1.776-18.832,27.573-21.103,71.29h-22.337
		V68.447H401.11V366.201z"
                                        />
                                    </g>
                                </svg>
                            </span>
                            <span class="radio-label">Grande</span>
                        </span>
                    </label>
                </div>
            </div>
            <div class="form-control w-full max-w-sm md:max-w-md lg:max-w-lg">
                <label for="" class="label">
                    <span class="label-text">Quali idee hai per la tela?</span>
                </label>
                <textarea
                    name="richiesta"
                    class="textarea textarea-bordered w-full max-w-sm md:max-w-md lg:max-w-lg"
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

    .radio-inputs {
        display: flex;
        justify-content: center;
        align-items: center;
        max-width: 350px;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    .radio-inputs > * {
        margin: 6px;
    }

    .radio-input:checked + .radio-tile {
        border-color: #2260ff;
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
        color: #2260ff;
    }

    .radio-input:checked + .radio-tile:before {
        transform: scale(1);
        opacity: 1;
        background-color: #2260ff;
        border-color: #2260ff;
    }

    .radio-input:checked + .radio-tile .radio-icon svg {
        fill: #2260ff;
    }

    .radio-input:checked + .radio-tile .radio-label {
        color: #2260ff;
    }

    .radio-input:focus + .radio-tile {
        border-color: #2260ff;
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1), 0 0 0 4px #b5c9fc;
    }

    .radio-input:focus + .radio-tile:before {
        transform: scale(1);
        opacity: 1;
    }

    .radio-tile {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 80px;
        min-height: 80px;
        border-radius: 0.5rem;
        border: 2px solid #b5bfd9;
        background-color: #fff;
        box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
        transition: 0.15s ease;
        cursor: pointer;
        position: relative;
    }

    .radio-tile:before {
        content: "";
        position: absolute;
        display: block;
        width: 0.75rem;
        height: 0.75rem;
        border: 2px solid #b5bfd9;
        background-color: #fff;
        border-radius: 50%;
        top: 0.25rem;
        left: 0.25rem;
        opacity: 0;
        transform: scale(0);
        transition: 0.25s ease;
    }

    .radio-tile:hover {
        border-color: #2260ff;
    }

    .radio-tile:hover:before {
        transform: scale(1);
        opacity: 1;
    }

    .radio-label {
        color: #707070;
        transition: 0.375s ease;
        text-align: center;
        font-size: 13px;
    }

    .radio-input {
        clip: rect(0 0 0 0);
        -webkit-clip-path: inset(100%);
        clip-path: inset(100%);
        height: 1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
    }
</style>
