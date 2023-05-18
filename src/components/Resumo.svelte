<div class="top-resumo">
    <h1>Resumo:</h1>
    <Frete/>
</div>
<div class="resumo">
    <p><strong>Items ({$globalCount})</strong></p>
    <p class='align'>R$ {$globalPrice}</p>
    <p><strong>Frete</strong></p>
    <p class='align'>{$globalFrete !== 0 ? 'R$ ' + $globalFrete : 'GRÁTIS'}</p>
    <p><strong>Total</strong></p>
    <p class='align'>R$ {$globalFrete + $globalPrice}</p>
</div>
<div class=button>
    <button on:click={() => handleSubmit()}>FINALIZAR PEDIDO</button>
</div>

<script lang="ts">
    import { getContext } from "svelte";
    import type { Writable } from "svelte/store";
    import Frete from "./Frete.svelte";

    let globalCount = getContext<Writable<number>>('gC');
    let globalPrice = getContext<Writable<number>>('gP');
    let globalFrete = getContext<Writable<number>>('gF');

    function handleSubmit(){
        if($globalCount === 0){
            alert("Adicione itens ao carrinho primeiro.")
            return;
        }
        alert("Pedido feito com sucesso!");
    }

</script>

<style>
    .top-resumo {
        margin: 3vw;
    }
    .resumo {
        display: grid;
        grid-template-columns: 50% 50%;
        margin: 3vw;
    }

    .align {
        justify-self: end;
    }

    .button {
        display: flex;
        justify-content: center;
    }

    button {
        border: none;
        color: rgb(108, 108, 108);
        background-color: #CACACA;
        width: 15vw;
        height: 4vh;
        border-radius: 0.5vw;
    }

    button:hover {
        cursor: pointer;
        color: #FAFAFA;
    }
</style>