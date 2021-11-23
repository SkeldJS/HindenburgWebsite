<script lang="ts">
    import navbarColor from "../stores/navbarColor";

    function cssColorToRgb(cssColor: string) {
        if (cssColor.startsWith("rgb(")) {
            return cssColor.substr(4).split(", ").map(part => parseInt(part));
        }

        const actualHex = cssColor.substr(1);

        return [ parseInt(actualHex.substr(0, 2), 16), parseInt(actualHex.substr(2, 4), 16), parseInt(actualHex.substr(4, 6), 16) ];
    }

    $: rgbColor = cssColorToRgb($navbarColor);
    $: textColor = rgbColor[0] * 0.299 + rgbColor[1] * 0.578 + rgbColor[2] * 0.114 > 186 ? "#000000" : "#ffffff";
</script>

<div class="navbar" style="background-color: {$navbarColor};">
    <div class="navbar-item title">
        <a href="/" style="color: {textColor};">Hindenburg</a>
    </div>
    <div class="navbar-item">
        <a href="/features" style="color: {textColor};">Features</a>
    </div>
    <div class="navbar-item">
        <a href="/guides" style="color: {textColor};">Guides</a>
    </div>
</div>

<div class="layout-page">
    <slot></slot>
</div>

<style>
    .navbar {
        box-shadow: 0px 2px 4px 0px rgba(0, 0, 0, 0.75);
        display: flex;
        padding-left: 15%;
        padding-right: 15%;
        position: fixed;
        width: 100vw;
        transition: background-color 0.2s;
        z-index: 99;
    }

    .navbar-item {
        padding: 18px;
    }

    .navbar-item > a {
        transition: color 0.4s;
    }

    .title {
        font-weight: 700;
    }
    
    @media screen and (max-width: 1080px) {
        .layout-page {
            padding-top: 48px;
        }
    }

    @media screen and (max-width: 580px) {
        .navbar {
            padding-left: 0%;
            padding-right: 0%;
            overflow-x: auto;
        }
    }
</style>