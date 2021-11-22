<script lang="ts">
    import navbarColor from "../stores/navbarColor";
    import CommandClodeBlock from "../components/CommandClodeBlock.svelte";

    const gitInstallLines = [
        "npm install -g yarn",
        "git clone https://github.com/skeldjs/Hindenburg",
        "cd Hindenburg",
        "yarn",
        "yarn setup",
        "yarn build",
        "yarn start"
    ];

    const dockerInstallLines = [
        "docker run\n--name Hindenburg\n-p 22023:22023/udp\nhindenburg/hindenburg:latest"
    ];

    let learnMoreChevron: HTMLImageElement;
    let learnMoreBeenHovered: boolean;
    function onLearnMoreHover() {
        learnMoreBeenHovered = true;
    }

    setTimeout(() => {
        if (!learnMoreChevron || learnMoreBeenHovered)
            return;

        learnMoreChevron.classList.add("play-bounce");
    }, 2000);

    let scrollY = 0;
    let splashContainer: HTMLDivElement;
    let featuresContainer: HTMLDivElement;
    let builtOnHindenburgContainer: HTMLDivElement;
    let publicIpContainer: HTMLDivElement;

    $: if (scrollY !== undefined) {
        const elements: (HTMLDivElement|undefined)[] = [ splashContainer, featuresContainer, builtOnHindenburgContainer, publicIpContainer ].reverse();
        for (const element of elements) {
            if (!element)
                continue;

            const boundingBox = element.getBoundingClientRect();
            if (boundingBox.top <= 50) {
                navbarColor.set(getComputedStyle(element, null).backgroundColor);
                break;
            }
        }
    }

    let ipTextbox: HTMLInputElement;

    function copyIp() {
        if (!ipTextbox) {
            return;
        }

        ipTextbox.select();
        document.execCommand("copy");
    }
</script>

<svelte:window bind:scrollY={scrollY} />

<div class="splash-container" bind:this={splashContainer}>
    <div class="splash-splitter">
        <div class="splash-hindenburg-description">
            <span class="splash-hindenburg">Hindenburg</span>
            <span class="splash-summary">The most powerful and extensible Among Us server.</span>
            <div class="splash-socials">
                <a href="https://github.com/skeldjs/Hindenburg" class="splash-social">
                    <img alt="github icon" src="/github-icon.png" width=32/>
                    <span class="social-name">Star on GitHub</span>
                </a>
                <a href="https://discord.gg/8ewNJYmYAU" class="splash-social">
                    <img alt="github icon" src="/discord-icon.png" width=32/>
                    <span class="social-name">Join our discord</span>
                </a>
                <a href="https://skeldjs.github.io/Hindenburg" class="splash-social">
                    <img alt="github icon" src="/book.svg" width=32/>
                    <span class="social-name">Read the docs</span>
                </a>
            </div>
        </div>
        <div class="splash-install-instructions">
            <CommandClodeBlock commandLines={gitInstallLines} />
            <span class="or">OR</span>
            <CommandClodeBlock commandLines={dockerInstallLines} />
        </div>
    </div>
    <a class="learn-more-container" href="#features" on:mouseover={onLearnMoreHover} on:focus={onLearnMoreHover}>
        <img
            class="learn-more-icon"
            bind:this={learnMoreChevron}
            alt="arrow facing downwards"
            src="/chevron.svg"
            width=24
        />
        <span class="learn-more-text">Why Hindenburg?</span>
    </a>
</div>
<div class="features-container" id="features" bind:this={featuresContainer}>
    <span class="features-header">Hindenburg is more than just an ordinary Among Us server.</span>
    <div class="feature-list">
        <div class="feature">
            <div class="feature-details">
                <span class="feature-name">Complete Authority</span>
                <p class="feature-description">Hindenburg does much more than a glorified relay server;
                    it actively participates and with Server-As-A-Host technology,
                    it provides full control over players, giving you huge amounts
                    of potential.</p>
            </div>
            <img class="feature-image" src="/servers.png" width=86 alt="authoratitive servers" />
        </div>
        <div class="feature rtl">
            <div class="feature-details">
                <span class="feature-name">Configurable</span>
                <p class="feature-description">You can customise almost every way in which Hindenburg works,
                    giving you the ability to fine-tune your server and make it perfect for your needs.</p>
            </div>
            <img class="feature-image" src="/settings.png" width=86 alt="authoratitive servers" />
        </div>
        <div class="feature">
            <div class="feature-details">
                <span class="feature-name">Plugins</span>
                <p class="feature-description">For server owners, seemlessly integrate easy-to-install plugins
                    into your server and configure them directly.

                    For plugin developers, Hindenburg's powerful API allows you to control everything from
                    individual rooms to the behaviour of the server itself. </p>
            </div>
            <img class="feature-image" src="/plug.png" width=86 alt="authoratitive servers" />
        </div>
    </div>
    <a class="learn-more-container margin" href="/features">
        <span class="learn-more-text">Check out the full list</span>
        <img
            class="learn-more-icon rotate"
            alt="arrow facing downwards"
            src="/chevron.svg"
            width=24
        />
    </a>
</div>
<div class="built-on-hindenburg-container" bind:this={builtOnHindenburgContainer}>
    <span class="built-on-hindenburg-header">Build with Hindenburg.</span>
    <div class="built-on-hindenburg-list">
        <div class="built-on-hindenburg">
            <div class="built-on-hindenburg-image mouthwash"></div>
            <div class="built-on-hindenburg-details">
                <a href="https://github.com/edqx/MouthwashGG" target="_blank" class="built-on-hindenburg-name">Mouthwash.gg</a>
                <p class="built-on-hindenburg-description">
                    Mouthwash.gg is an open-source re-implementation of the Polus.gg back-end.
                    It uses Hindenburg's plugin API to its potential, making use of custom client-server protocol
                    additions and new InnerNet objects, and develops an API on-top to
                    create roles and entire gamemodes in a modular fashion.
                </p>
            </div>
        </div>
        <div class="built-on-hindenburg rtl">
            <div class="built-on-hindenburg-image skeld-net"></div>
            <div class="built-on-hindenburg-details">
                <a href="https://skeld.net" target="_blank" class="built-on-hindenburg-name">skeld.net</a>
                <p class="built-on-hindenburg-description">
                    Skeld.net is a free public Among Us server, adding lots to base Among Us
                    without any client modifications. With Hindenburg's Server-As-A-Host technology,
                    it allows for much more control and power to create new and exciting gamemodes.
            </div>
        </div>
    </div>
    <a class="learn-more-container margin" href="/get-started">
        <span class="learn-more-text">Be the next</span>
        <img
            class="learn-more-icon rotate"
            alt="arrow facing downwards"
            src="/chevron.svg"
            width=24
        />
    </a>
</div>
<div class="public-ip-container" bind:this={publicIpContainer}>
    <span class="public-ip-header">Ready to give it a spin?</span>
    <!--<div class="public-ip">
        <p>Check out the public Hindenburg instance:</p>
        <div class="ip-address-container">
            <input class="ip-address" bind:this={ipTextbox} value="127.0.0.1" readonly />
            <img on:click={copyIp} class="copy-to-clipboard" src="/content-copy.svg" alt="copy to clipboard" />
        </div>
    </div>-->
    <a class="learn-more-container margin" href="/get-started">
        <span class="learn-more-text">Get started</span>
        <img
            class="learn-more-icon rotate"
            alt="arrow facing downwards"
            src="/chevron.svg"
            width=24
        />
    </a>
</div>
<div class="footer-container">
    <span class="footer-hindenburg">Hindenburg</span>
    <div class="footer-list">
        <div class="footer-item">
            <span class="footer-header">Socials</span>
            <a href="https://github.com/skeldjs/Hindenburg">GitHub</a>
            <a href="https://hub.docker.com/r/hindenburg/hindenburg">DockerHub</a>
            <a href="https://discord.gg/8ewNJYmYAU">Discord</a>
        </div>
        <div class="footer-item">
            <span class="footer-header">Icons</span>
            <a href="https://materialdesignicons.com">Material Design Icons</a>
            <a href="https://flaticon.com">Flaticon</a>
            <a href="https://heroicons.com">Heroicons</a>
        </div>
    </div>
    <span class="made-with">Made with ♥ by <a href="https://github.com/edqx">edqx</a></span>
</div>

<style>
    .splash-container {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        justify-content: center;
        align-items: center;
        background-color: var(--main-bg-color);
    }

    .splash-splitter {
        margin-left: 160px;
        margin-right: 160px;
        display: flex;
        justify-content: space-around;
        width: 100%;
    }

    .splash-splitter > div {
        min-width: 400px;
        margin: 80px;
    }

    .splash-hindenburg-description {
        display: flex;
        flex-direction: column;
    }

    .splash-hindenburg {
        font-weight: 700;
        font-size: 46px;
        margin-bottom: 8px;
    }

    .splash-socials {
        margin-top: 80px;
        display: flex;
        flex-direction: column;
    }

    .splash-social {
        margin-top: 15px;
        display: flex;
        align-items: center;
    }

    .social-name {
        margin-left: 16px;
    }

    .or {
        display: block;
        text-align: center;
        font-weight: 700;
        margin-top: 15px;
        margin-bottom: 15px;
    }

    .learn-more-container {
        display: flex;
        align-items: center;
    }
    
    .learn-more-container.margin {
        margin-top: 80px;
    }

    .learn-more-icon {
        animation-duration: 1s; 
        animation-fill-mode: both; 
    }

    .learn-more-text {
        margin-left: 8px;
    }

    .learn-more-icon.rotate {
        transform: rotate(-90deg);
    }

    .features-container {
        background-color: #4e718c;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 80px;
        padding-bottom: 80px;
    }

    .features-header {
        margin: 80px;
        text-align: center;
        font-size: 34px;
        font-weight: 700;
        max-width: 720px;
    }

    .feature-list {
        display: flex;
        flex-direction: column;
    }

    .feature {
        display: flex;
        align-items: center;
        width: 800px;
    }

    .feature > * {
        margin: 40px;
    }

    .feature.rtl {
        flex-direction: row-reverse;
    }

    .feature-name {
        font-weight: 700;
        font-size: 24px;
    }

    .feature-details {
        display: flex;
        flex-direction: column;
        flex: 4 1 0;
    }

    .built-on-hindenburg-container {
        background-color: #1a3951;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 80px;
        padding-bottom: 80px;
    }

    .built-on-hindenburg-header {
        margin: 80px;
        text-align: center;
        font-size: 34px;
        font-weight: 700;
        max-width: 720px;
    }

    .built-on-hindenburg {
        display: flex;
    }

    .built-on-hindenburg:not(:first-child) {
        margin-top: 80px;
    }

    .built-on-hindenburg.rtl {
        flex-direction: row-reverse;
    }

    .built-on-hindenburg-image {
        border-radius: 16px;
        position: relative;
        border-radius: 16px;
        width: 480px;
        height: 270px;
        border: 2px solid black;
    }

    .built-on-hindenburg-image.mouthwash {
        background-image: linear-gradient(to right, rgba(0, 0, 0, 0) 0px, rgba(0, 0, 0, 0.3) 100%),
            url("https://user-images.githubusercontent.com/60631511/140629842-4ef52dc1-cbef-4b50-8b4a-caef1f4d4350.png");
        background-size: cover;
    }

    .built-on-hindenburg-image.skeld-net {
        background-image: linear-gradient(to left, rgba(0, 0, 0, 0) 0px, rgba(0, 0, 0, 0.3) 100%),
            url("https://via.placeholder.com/480x270");
        background-size: cover;
    }

    .built-on-hindenburg-details {
        margin-top: 30px;
        margin-left: 20px;
    }

    .built-on-hindenburg-name {
        font-size: 24px;
        font-weight: 700;
    }

    .built-on-hindenburg-description {
        max-width: 450px;
    }
    
    .public-ip-container {
        background-color: var(--main-bg-color);
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 80px;
        padding-bottom: 80px;
    }

    .public-ip-header {
        margin-top: 20px;
        text-align: center;
        font-size: 34px;
        font-weight: 700;
        max-width: 720px;
    }

    .public-ip {
        text-align: center;
    }

    .ip-address-container {
        display: flex;
    }

    .ip-address {
        background-color: #0a0a0a;
        border: 1px solid black;
        border-radius: 16px;
        padding: 16px;
        font-size: 13px;
        font-family: "Source Code Pro", monospace;
        max-width: 450px;
        flex: 1 1 0;
        color: white;
        text-align: center;
        margin-right: 14px;
    }

    .copy-to-clipboard {
        cursor: pointer;
    }
    
    .footer-container {
        background-color: black;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 40px;
        padding-bottom: 40px;
    }

    .footer-hindenburg {
        font-size: 24px;
        font-weight: 700;
    }

    .footer-header {
        text-decoration: underline;
        margin-top: 20px;
        margin-bottom: 10px;
    }

    .footer-list {
        display: flex;
    }

    .footer-item {
        display: flex;
        flex-direction: column;
        margin-left: 30px;
        margin-right: 30px;
    }

    .made-with {
        margin-top: 30px;
    }

    @media screen and (max-width: 1080px) {
        .splash-container {
            margin-bottom: 80px;
        }

        .splash-splitter {
            flex-direction: column;
            justify-content: start;
            align-items: center;
        }

        .splash-splitter > div {
            min-width: 200px;
            margin: 30px;
        }

        .feature {
            width: auto;
        }

        .feature-description {
            max-width: 600px;
        }

        .built-on-hindenburg {
            flex-direction: column;
            align-items: center;
        }

        .built-on-hindenburg.rtl {
            flex-direction: column;
        }
    }
    
    @media screen and (max-width: 580px) {
        .splash-socials {
            margin-top: 40px;
        }

        .features-header {
            font-size: 24px;
            margin-left: 20px;
            margin-right: 20px;
        }

        .built-on-hindenburg-header {
            font-size: 24px;
            margin-left: 20px;
            margin-right: 20px;
        }

        .public-ip-header {
            font-size: 24px;
            margin-left: 20px;
            margin-right: 20px;
        }

        .feature, .feature.rtl {
            flex-direction: column-reverse;
            margin-bottom: 40px;
        }

        .feature > * {
            margin: 10px;
            margin-left: 30px;
            margin-right: 30px;
        }

        .built-on-hindenburg-image {
            width: 320px;
            height: 180px;
        }
    }
</style>