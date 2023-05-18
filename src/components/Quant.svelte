<div class="container">
    <button class="minus" on:click={() => dispatch('minusClicked', 0)}>-</button>
    <p>{quant}</p>
    <button class="plus" on:click={() => dispatch('plusClicked', 1)}>+</button>
</div>

<script lang="ts">    
    import { createEventDispatcher } from "svelte";

    export let quant: number;

    const dispatch = createEventDispatcher();

</script>

<style>
    .container {
        display: flex;
        gap: 1vw;
        margin: 0.1vw;
        border-radius: 0.25vw;
        background-color: rgb(243, 243, 243);
        height: 90%;
        align-items: center;
    }

    .minus, .plus {
        text-align: center;
        background-color: rgb(211, 211, 211);
        width: 1.5vw;
        height: 90%;
        border-radius: 0.25vw;
        border: none;
    }

    .minus:hover, .plus:hover {
        cursor: pointer;
        box-shadow: 0px 0px 1px 1px #FAFAFA;
    }
</style>