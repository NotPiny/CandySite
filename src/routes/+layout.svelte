<script>
    // import CandyWebp from '$lib/images/CandySmall.webp';
    // import CandyPng from '$lib/images/CandySmall.png';
    import navLeft from '$lib/images/navRoundLeft.svg';
    import navRight from '$lib/images/navRoundRight.svg';
    import github from '$lib/images/github.svg';
    import { page } from '$app/stores';
    import { onMount } from 'svelte';

    let platform = 'desktop';

    onMount(async() => {
        if (window.innerWidth < 768) {
            platform = 'mobile';
        }
    })

    const links = [
        { name: 'Home', href: '/' },
        { name: 'About', href: '/About' },
    ];

    let heartHover = false;
    let lastAlert = 0;

    /**
     * @param {string} message
     * @param {number} delay
     */
    async function tryAlert(message, delay) {
        if (heartHover) {
            setTimeout(() => {
                if (heartHover && lastAlert + delay < Date.now()) {
                    alert(message);
                    lastAlert = Date.now();
                }
            }, delay);
        }
    }
</script>

<div class="nav">
    <!-- <picture>
        <source srcset={CandyWebp} type="image/webp">
        <img src={CandyPng} alt="Candy Logo" >
    </picture> -->
    {#if platform === 'desktop'}
        <h2>Candy</h2>
    {/if}
    {#if platform === 'mobile'}
        <h2>CNDY</h2>
    {/if}
    <div class="links">
        <img src={navLeft} alt="navLeft" />
        {#each links as link}
            <a href={link.href}
                class:no-border={link === links[links.length - 1] || link.href === $page.route.id || links.length == 2}
                class:selected={link.href === $page.route.id}
            >{link.name}</a>
        {/each}
        <img src={navRight} alt="navRight" />
    </div>
    <a href="https://github.com/NotPiny/Candy" target="_blank" style="position: absolute; right: 1rem; top: 2.5%;">
        <img src={github} alt="github" width="35" height="35"/>
    </a>
</div>

<div class="wrapper">
    <slot/>
</div>

<div class="footer">
    <p>
        <!-- svelte-ignore a11y-no-static-element-interactions -->
        Made with <span 
            on:mouseenter={() => {
                heartHover = true;
                tryAlert('Olilz is such a bot 🤖', 2.5 * 1000);
            }}
            on:mouseleave={() => {
                heartHover = false;
            }}
        >❤️</span> by <a href="https://piny.dev" target="_blank">Piny</a><br/>
        Icons from <a href="https://tabler.io/icons" target="_blank">Tabler Icons</a>
    </p>
</div>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Lilita+One&display=swap');
    :root {
        --color-primary: #87999E;
        --color-text: #d9d9d9;
        --color-secondary: #1e1e1e;
    }

    .nav {
        display: flex;
        justify-content: start;

        margin: 0;
        height: 85px;
        padding: .15rem;

        background-color: var(--color-primary);
    }

    .nav h2 {
        font-family: Lilita One, sans-serif;
        font-size: 2rem;
        font-weight: 700;
        color: var(--color-text);
        margin: 0;
        padding-top: 1.35rem;
        padding-left: 1rem;
    }

    .nav .links {
        position: absolute;
        display: flex;
        justify-content: center;
        align-items: center;

        width: 100%;
        height: 85px;
    }
    
    .nav .links a {
        border-right: 1px solid var(--color-secondary);

        color: var(--color-secondary);
        text-decoration: none;
        font-weight: bold;
        text-align: center;

        padding: 1rem;
        background-color: #fff;
    }

    .nav .links a:hover {
        background-color: #dddddd !important;
    }

    .nav .selected {
        background-color: #ebebeb !important;
        color: #fff;
    }

    /* .nav picture {
        width:80px;
        height:50px;

        position: absolute;
        left: 1rem;
        top: 1rem;

        margin-right: 1rem;
    } */

    .no-border {
        border-right: none !important;
    }

    .wrapper {
        margin: 0;
        padding: 1rem;
    }

    .footer {
        display: flex;
        justify-content: center;
        align-items: center;

        margin: 0;
        height: 85px;
        padding: .15rem;

        background-color: var(--color-primary);

        width: 100%;
    }

    .footer p {
        color: var(--color-text);
        font-size: 1rem;
        font-weight: bold;
        text-align: center;
    }

    .footer a {
        color: rgb(223, 223, 223);
    }
</style>