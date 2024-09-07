<script>
    import { browser } from "$app/environment";
    import { onMount } from "svelte";

    let heartHover = false;
    let lastAlert = 0;

    // Yes this is stolen from the main layout file but I don't think it's worth making into a component
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

    onMount(() => {
        const text = document.querySelector('.galaxy-text');
        if (!text) return;
        const textContent = text.innerHTML;
        if (!textContent) return; // Huh? Why would this be null?

        const splitText = textContent.split('');
        text.innerHTML = '';

        splitText.forEach((char, i) => {
            setTimeout(() => {
                text.innerHTML += char;
            }, 75 * i);
        });
    })
</script>

<h1><span class="galaxy-text">Hey there!</span> 👋</h1>
<p style="margin-top: 0; font-weight: bold; font-size: 1.3rem;">
    This is Candy - a Free and Open Source Discord user app designed to make the Discord experience better.
</p>
<h2>
    Why does this exist?
</h2>
<p>
    I created Candy because I wanted to a) learn more about how discord user apps work and b) make the Discord experience better for myself and others.
</p>
<h2>
    Can I self host / modify this?
</h2>
<p>
    Yes! Candy doesn't have any form of license attached to its source code <a href="https://github.com/NotPiny/Candy?tab=readme-ov-file#license" target="_blank">(apart from this)</a>. You can find the source code at <a href="https://github.com/NotPiny/Candy" target="_blank">NotPiny/Candy on GitHub</a> the readme should have all the information you need to get started under the <a href="https://github.com/NotPiny/Candy?tab=readme-ov-file#developer-stuff" style="color: white;" target="_blank"><code>Developer stuff</code> heading</a>.
</p>
<h2>
    The details behind the app
</h2>
<p>
    Candy is built using <a href="https://discord.js.org" target="_blank">discord.js</a> and <a href="https://axios-http.com/" target="_blank">axios</a>. That's it. It's meant to be simple and easy to work with. The official Candy bot is hosted on <a href="https://daalbot.xyz">DaalBot's</a> server as well I don't want to buy another server just for this.
</p>
<h2>
    How can I contribute?
</h2>
<p>
    Like said in the readme on the GitHub repo, you can contribute by making a pull request with your changes. And I will review them as soon as I can. If you have any questions, feel free to ask in <a href="https://go.daalbot.xyz/HQ">DaalBot's support server</a>.
</p>
<h2>
    Why the name "Candy"?
</h2>
<p>
    <!-- svelte-ignore a11y-no-static-element-interactions -->
    To be honest, I don't really know. I came up with it when I was thinking of a new name for my twitch bot and decided to go with <span id="cndy-is-cindy" on:mouseenter={() => {
        if (browser) {
            heartHover = true;
            tryAlert('Fun fact: It\'s real name is actually Cindy', 2.5 * 1000);

            const ele = document.getElementById('cndy-is-cindy');
            if (!ele) return;

            ele.style.color = '#d2d2d2';
        }
    }}
    on:mouseleave={() => {
        if (browser) {
            heartHover = false;

            const ele = document.getElementById('cndy-is-cindy');
            if (!ele) return;

            ele.style.color = '#fff';
        }
    }}>CndyBot</span> (used to be DaalBotT). Which was the inspiration for the whole app so why not keep the name?
</p>
<h2>
    Okay cool cool, but what the hell is DaalBot and why do you keep mentioning it?
</h2>
<p>
    Well thank you for asking (even though you didn't). DaalBot is a Discord bot that I made and maintain. It's a general purpose bot designed to be infinitely customisable and is how Candy was born. You can find out more about DaalBot at <a href="https://daalbot.xyz" target="_blank">daalbot.xyz</a>.
</p>

<svelte:head>
    <title>
        Candy | About
    </title>
    <meta name="description" content="Learn more about Candy and why it exists." />
    <style>
        .wrapper {
            margin: 2rem;
        }
    </style>
</svelte:head>

<style>
    h1 {
        font-size: 5rem;
        font-weight: bold;
        margin-bottom: .3rem;
        margin-top: 0;
    }

    h2 {
        font-size: 2rem;
        font-weight: bold;
        margin-top: 3rem;
        margin-bottom: 1rem;
    }

    a {
        color: #fff;
        text-decoration: underline;
    }

    a:visited {
        color: #d9d9d9;
    }

    .galaxy-text {
        background: linear-gradient(45deg, #4b0082, #8a2be2, #000080, #483d8b, #2e0854);
        background-size: 200% 200%;
        background-clip: text;
        color: transparent;
        animation: galaxyAnimation 6s ease-in-out infinite;
        text-shadow: 0 0 10px rgba(138, 43, 226, 0.5), 0 0 20px rgba(75, 0, 130, 0.3);
    }

    @keyframes galaxyAnimation {
        0% { background-position: 0% 50%; }
        50% { background-position: 100% 50%; }
        100% { background-position: 0% 50%; }
    }

    code {
        background: #000;
        color: #fff;
        padding: 0.25rem;
        border-radius: 0.25rem;
    }
</style>