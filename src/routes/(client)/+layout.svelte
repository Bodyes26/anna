<script>
    import "../../app.css";
    let background;
</script>

<div class="navbar bg-base-100 lg:px-8 pl-4 pr-8 pt-4">
    <div class="navbar-start">
        <div class="dropdown">
            <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
            <label for="" tabindex="0" class="btn btn-ghost lg:hidden">
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    class="h-5 w-5"
                    fill="none"
                    viewBox="0 0 24 24"
                    stroke="currentColor"
                    ><path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        stroke-width="2"
                        d="M4 6h16M4 12h8m-8 6h16"
                    /></svg
                >
            </label>
            <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
            <ul
                tabindex="0"
                class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52"
            >
                <li><a href="/portfolio">Portfolio</a></li>
                <li><a href="/shop">Shop</a></li>
            </ul>
        </div>
        <a class="logo" href="/"> Anna.rt </a>
    </div>
    <div class="navbar-center hidden lg:flex">
        <ul class="menu menu-horizontal px-1">
            <li><a href="/portfolio">Portfolio</a></li>
            <li><a href="/shop">Shop</a></li>
        </ul>
    </div>
    <div class="navbar-end">
        <a href="/contatti" class="button btn-1">Contatti</a>
    </div>
</div>

<slot />

<footer class="footer footer-center p-10 mt-12">
    <div>
        <div
            class="w-20 h-fit rounded-lg"
            style="background-image: url('/images/logo_smol.png'); background-size: cover; background-position: center;"
            bind:this={background}
        >
            <img
                src="images/logo.png"
                alt="logo"
                class=" rounded-lg"
                on:load={() => {
                    background.style.backgroundImage = "none";
                }}
            />
        </div>

        <p class="font-bold">
            Anna.rt <br />Making art for passion
        </p>
        <p>Copyright © 2023 - Tutti i diritti riservati</p>
    </div>
    <div>
        <div class="grid grid-flow-col gap-4">
            <a href="https://www.instagram.com/_anna.rt/"
                ><svg
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                >
                    <path
                        fill-rule="evenodd"
                        clip-rule="evenodd"
                        d="M12 18C15.3137 18 18 15.3137 18 12C18 8.68629 15.3137 6 12 6C8.68629 6 6 8.68629 6 12C6 15.3137 8.68629 18 12 18ZM12 16C14.2091 16 16 14.2091 16 12C16 9.79086 14.2091 8 12 8C9.79086 8 8 9.79086 8 12C8 14.2091 9.79086 16 12 16Z"
                        fill="#0F0F0F"
                    />
                    <path
                        d="M18 5C17.4477 5 17 5.44772 17 6C17 6.55228 17.4477 7 18 7C18.5523 7 19 6.55228 19 6C19 5.44772 18.5523 5 18 5Z"
                        fill="#0F0F0F"
                    />
                    <path
                        fill-rule="evenodd"
                        clip-rule="evenodd"
                        d="M1.65396 4.27606C1 5.55953 1 7.23969 1 10.6V13.4C1 16.7603 1 18.4405 1.65396 19.7239C2.2292 20.8529 3.14708 21.7708 4.27606 22.346C5.55953 23 7.23969 23 10.6 23H13.4C16.7603 23 18.4405 23 19.7239 22.346C20.8529 21.7708 21.7708 20.8529 22.346 19.7239C23 18.4405 23 16.7603 23 13.4V10.6C23 7.23969 23 5.55953 22.346 4.27606C21.7708 3.14708 20.8529 2.2292 19.7239 1.65396C18.4405 1 16.7603 1 13.4 1H10.6C7.23969 1 5.55953 1 4.27606 1.65396C3.14708 2.2292 2.2292 3.14708 1.65396 4.27606ZM13.4 3H10.6C8.88684 3 7.72225 3.00156 6.82208 3.0751C5.94524 3.14674 5.49684 3.27659 5.18404 3.43597C4.43139 3.81947 3.81947 4.43139 3.43597 5.18404C3.27659 5.49684 3.14674 5.94524 3.0751 6.82208C3.00156 7.72225 3 8.88684 3 10.6V13.4C3 15.1132 3.00156 16.2777 3.0751 17.1779C3.14674 18.0548 3.27659 18.5032 3.43597 18.816C3.81947 19.5686 4.43139 20.1805 5.18404 20.564C5.49684 20.7234 5.94524 20.8533 6.82208 20.9249C7.72225 20.9984 8.88684 21 10.6 21H13.4C15.1132 21 16.2777 20.9984 17.1779 20.9249C18.0548 20.8533 18.5032 20.7234 18.816 20.564C19.5686 20.1805 20.1805 19.5686 20.564 18.816C20.7234 18.5032 20.8533 18.0548 20.9249 17.1779C20.9984 16.2777 21 15.1132 21 13.4V10.6C21 8.88684 20.9984 7.72225 20.9249 6.82208C20.8533 5.94524 20.7234 5.49684 20.564 5.18404C20.1805 4.43139 19.5686 3.81947 18.816 3.43597C18.5032 3.27659 18.0548 3.14674 17.1779 3.0751C16.2777 3.00156 15.1132 3 13.4 3Z"
                        fill="#0F0F0F"
                    />
                </svg></a
            >
        </div>
    </div>
</footer>

<style>
    @font-face {
        font-family: "Paragon";
        src: url("/fonts/Paragon_italic.otf");
    }

    .logo {
        font-family: "Paragon", serif;
        font-size: larger;
    }

    .button {
        text-decoration: none;
        padding: 10px 30px;
        font-size: 1em;
        position: relative;
        border: none;
        background-color: #6ab6bc;
        font-weight: 600;
    }

    .btn-1 {
        overflow: hidden;
        color: #000;
        border-radius: 30px;
        box-shadow: 0 0 0 0 rgba(143, 64, 248, 0.5),
            0 0 0 0 rgba(39, 200, 255, 0.5);
        transition: transform 0.3s ease, box-shadow 0.3s ease, color 0.3s ease;
    }

    .btn-1::after {
        content: "";
        width: 400px;
        height: 400px;
        position: absolute;
        top: -50px;
        left: -100px;
        background-color: #a7d7d8;
        background-image: linear-gradient(
            225deg,
            #27d86c 0%,
            #a7d7d8 50%,
            #c625d0 100%
        );
        z-index: -1;
        transition: transform 0.5s ease;
    }

    .btn-1:hover {
        transform: translate(0, -6px);
        color: #fff;
        box-shadow: 10px -10px 25px 0 rgba(143, 64, 248, 0.5),
            -10px 10px 25px 0 rgba(39, 200, 255, 0.5);
    }

    .btn-1:hover::after {
        transform: rotate(150deg);
    }
</style>
