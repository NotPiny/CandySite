<script>
    import { browser } from '$app/environment';
    import CandySvg from '$lib/images/CandySweet.svg';
    import GroupIcon from '$lib/images/group.svg';
    import UserIcon from '$lib/images/user.svg';
    import heartsIcon from '$lib/images/hearts.svg';
    import toolIcon from '$lib/images/tool.svg';
    import dotsIcon from '$lib/images/dots.svg';
    import { onMount } from 'svelte';

    let platform = 'desktop';

    onMount(() => {
        if (window.innerWidth < 1905) {
            platform = 'mobile';
        }
        /**
         * @type {HTMLDivElement | null}
        */
        const wrapper = document.querySelector('.wrapper'); // Get the wrapper element (defined in +layout.svelte)
        if (!wrapper) return;

        wrapper.style.opacity = '0'; // Set the opacity to 0

        let opacity = 0; // Set the initial opacity to 0

        const interval = setInterval(() => {
            opacity += 0.01; // Increment the opacity by 0.01
            wrapper.style.opacity = opacity.toString(); // Set the opacity to the new value

            if (opacity >= 1) { // If the opacity is greater than or equal to 1
                clearInterval(interval); // Clear the interval
            }
        }, 10); // Run the interval every 10ms
    })

    const features = [
        {
            title: 'Roleplay',
            description: `Who doesn't like to roleplay a little?`,
            image: heartsIcon
        },
        {
            title: 'Utility',
            description: `Like a swiss army knife, but for discord.`,
            image: toolIcon
        },
        {
            title: 'Miscellaneous',
            description: `A little bit of everything.`,
            image: dotsIcon
        }
    ];
</script>

<svelte:head>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/components/carousel-item/carousel-item.js"></script>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/components/carousel/carousel.js"></script>
    <script type="module" src="https://cdn.jsdelivr.net/npm/@shoelace-style/shoelace@2.16.0/cdn/components/icon/icon.js"></script>

    <title>Candy</title>
    <meta name="description" content="Candy is a free and open source user app for discord designed to make your discord experience better.">
</svelte:head>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="invite-selector" style="display: none;">
    <span class="invite-selector-bg" on:click={() => {
        /**
         * @type {HTMLDivElement | null}
        */
        const inviteSelector = document.querySelector('.invite-selector');
        if (!inviteSelector) return; // How the hell did this happen?
        inviteSelector.style.display = 'none';
    }}/>

    <div class="invite-selector-content">
        <h1>Add Candy</h1>
        <p>
            How would you like to add Candy?
        </p>
        <div class="invite-selector-button-split">
            <a href="https://go.candy.piny.dev/Install">
                <div class="invite-selector-button">
                    <img src="{UserIcon}" alt="Icon with a person"/>
                    <h3>Account</h3>
                    <p>Add Candy directly<br/>to your account.</p>
                    <p class="subtext">(Recommended)</p>
                </div>
            </a>
            <a href="https://go.candy.piny.dev/Invite">
                <div class="invite-selector-button">
                    <img src="{GroupIcon}" alt="Icon with a group of people"/>
                    <h3>Server</h3>
                    <p>Add Candy to a<br/>whole server.</p>
                    <p class="subtext" style="font-size:xx-small;">
                        (Requires Manage Server)
                    </p>
                </div>
            </a>
        </div>
    </div>
</div>

<div class="content">
    <div class="intro">
        <div class="intro-text">
            <h1>Candy - Redefining discord apps</h1>
            <p>
                Candy is a simple yet powerful user app designed to make discord better with features and commands that can be used in any server.
            </p>
        </div>
        <div class="intro-actions">
            <button on:click={() => {
                if (!browser) return; // No SSR >:(
                /**
                 * @type {HTMLDivElement | null}
                */
                const inviteSelector = document.querySelector('.invite-selector');
                if (!inviteSelector) return; // How the hell did this happen?
                inviteSelector.style.display = 'block';
    
            }}>Get Started</button>
        </div>
        <div class="intro-image">
            <img src={CandySvg} alt="Candy Logo" width="300" height="300"/>
        </div>
    </div><br/>

    <div class="feature-area">
        <h1>
            Features
        </h1>
        <!-- svelte-ignore a11y-mouse-events-have-key-events -->
        {#each features as feature}
            <!-- svelte-ignore a11y-no-static-element-interactions -->
            <div class="feature-card" id="feature-card-{feature.title.toLowerCase()}" on:mouseover={() => {
                // // Lift the card up
                // /**
                //  * @type {HTMLDivElement | null}
                // */
                // // @ts-ignore
                // const card = document.getElementById(`feature-card-${feature.title.toLowerCase()}`);
                // if (!card) return;
                // card.style.transform = 'translateY(-10px)';
            }}>
                <h2>{feature.title}</h2>
                <p>{feature.description}</p>
                {#if feature.image && platform === 'desktop'}
                    <img src={feature.image} alt={feature.title} width="360" height="255"/>
                {/if}
            </div>
        {/each}
    </div>
    
    <div class="faq">
        <h2>
            Frequently Asked Questions
        </h2>
    
        <div class="faq-list">
            <details>
                <summary>Why user apps?</summary>
                <p>
                    Simply put, traditional bots are limited in the way that you can only use their features inside of a server that they are in. User apps are different and can be used in any server or dm that you have access to.
                </p>
            </details>
    
            <details>
                <summary>How do I add Candy?</summary>
                <p>
                    You can add Candy to your account or a server by clicking the button below.
                </p>
            </details>
        </div>
    </div>
</div>

<style>
    .content {
        margin-left: 10%;
        margin-top: 5%;
    }

    .intro {
        margin-bottom: 10rem;
    }

    .intro-text h1 {
        font-size: 2.5rem;
        font-weight: 700;

        margin-bottom: .75rem;
    }

    .intro-text p {
        font-size: 1.1rem;
        font-weight: 400;
    }

    .intro-image {
        position: absolute;
        right: 10%;
        top: 16%;

        background-color: #87999E;

        height: 320px;
        width: 320px;

        display: flex;
        justify-content: center;
        align-items: center;

        border-radius: 10px;
    }

    .intro-actions button {
        background-color: #fff;
        color: #1e1e1e;
        border: none;
        border-radius: 5px;
        padding: 1rem;
        font-size: 1.2rem;
        font-weight: 700;

        cursor: pointer;
    }

    .intro-actions button:hover {
        transition: all 0.7s;
        background-color: #1e1e1e;
        color: #fff;
    }

    .intro-actions button:not(:hover) {
        transition: all 1.7s;
        background-color: #fff;
        color: #1e1e1e;
    }

    .invite-selector {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 1;

        display: flex;
        justify-content: center;
        align-items: center;
    }

    .invite-selector-bg {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        z-index: 0;

        background-color: rgba(0, 0, 0, 0.5);
    }

    .invite-selector-content {
        position: fixed;
        z-index: 1;

        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);

        background-color: rgba(0, 0, 0, 0.2);
        border-radius: 10px;
        padding: 1rem;

        text-align: center;
    }

    .invite-selector-content h1 {
        font-weight: 700;
        margin-top: 0;
        margin-bottom: .5rem;
    }

    .invite-selector-button-split {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .invite-selector-button-split a {
        color: #fff;
        text-decoration: none;
    }

    .invite-selector-button {
        background-color: rgba(0, 0, 0, 0.3); /* Just stacking these to infinity ig */
        border-radius: 10px;
        padding: 2rem;
        margin: .5rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        cursor: pointer;
    }

    .invite-selector-button img {
        border-radius: 50%;

        width: 100px;
        height: 100px;

        margin-bottom: 1rem;
    }

    .invite-selector-button h3 {
        font-weight: 700;
        margin-top: 0;
        margin-bottom: .5rem;
    }

    .invite-selector-button p {
        margin-top: 0;
        margin-bottom: 0;
    }

    .invite-selector-button .subtext {
        font-size: .75rem;
        margin-top: .3rem;
        font-weight: 500;
    }

    details {
        margin: 1rem;
        padding: 1rem;
        border: 1px solid #ccc;
        border-radius: 5px;

        width: 80%;
    }

    details p {
        font-size: 1.1rem;
        font-weight: 500;
    }

    summary {
        font-size: 1.5rem;
        font-weight: 700;

        cursor: pointer;
        text-align: center;
    }

    .feature-area {
        width: 85%;
        /* height: 10rem; */
    }

    .feature-area h1 {
        font-size: 2rem;
        font-weight: 700;
        margin-bottom: .1rem;
    }

    .feature-card {
        margin-bottom: 2rem;

        padding: 1rem;
        border: 1px solid #ccc;
        border-radius: 15px;
        background-color: var(--color-secondary);
    }

    .feature-card h2 {
        font-size: 1.5rem;
        font-weight: 700;
        margin-bottom: .5rem;
        margin-top: .25rem;
    }

    @media (max-width: 1905px) {
        .content {
            margin-left: 5%;
            margin-top: 5%;
        }

        .intro-image {
            display: none;
        }
    }

    @media (min-width: 1905px) {
        .feature-area {
            flex-direction: row !important;
            justify-content: space-between;
        }

        .feature-card {
            max-width: fit-content;
            display: inline-block;

            margin: 1rem;
        }

        .feature-card:hover {
            transition: all 0.5s;
            transform: translateY(-10px);
        }

        .feature-card:not(:hover) {
            transition: all 1.5s;
            transform: translateY(0);
        }
    }
</style>