<script lang="ts">
    import navbarColor from "../stores/navbarColor";
</script>

<div class="navbar" style="background-color: {$navbarColor}">
    <div class="navbar-item title">
        <a href="/">Hindenburg</a>
    </div>
    <div class="navbar-item">
        <a href="/features">Features</a>
    </div>
    <div class="navbar-item">
        <a href="/guides">Guides</a>
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