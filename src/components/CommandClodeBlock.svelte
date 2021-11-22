<script lang="ts">
    export let commandLines: string[];
</script>

<div class="command-code-block">
    {#each commandLines as command}
        <span class="command-line">
            <span class="prefix">$</span>
            <span class="command-keyword">{command.split(" ")[0]}</span>
            {#if command.indexOf(" ") > -1}
                {#each command.substr(command.indexOf(" ")).split("\n") as line, i}
                    {#if i > 0}
                        &nbsp;\<br>
                    {/if}
                    <span class:indent={i > 0}>{line}</span>
                {/each}
            {/if}
        </span>
    {/each}
</div>

<style>
    .command-code-block {
        display: flex;
        flex-direction: column;
        background-color: #0a0a0a;
        border: 1px solid black;
        border-radius: 16px;
        padding: 16px;
        font-size: 13px;
        font-family: "Source Code Pro", monospace;
        max-width: 450px;
    }

    .prefix {
        color: #363636;
        user-select: none;
    }
    
    .command-keyword {
        color: #ffbf00;
    }

    .indent {
        margin-left: 40px;
    }
    
    @media screen and (max-width: 1080px) {
        .command-code-block {
            width: auto;
        }
    }
</style>

