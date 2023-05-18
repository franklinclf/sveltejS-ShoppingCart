<div class="item-container">
    <div>
        <img src={image} alt="Imagem do produto">
        <button on:click={() => handleErase()}>✕</button>
    </div>
    <div class="info-container">
        <p><strong>{nome}</strong></p>
        <p>{desc}</p>
        <div class="quant-container">
            <p><strong>R$ {price * quant}</strong></p>
            <Quant {quant} on:minusClicked={() => handleClick(0)} on:plusClicked={() => handleClick(1)}/>
        </div>
    </div>
</div>

<script lang="ts">
    import { getContext } from "svelte";
    import type { Writable } from "svelte/store";
    import Quant from "./Quant.svelte";
    export let nome: string;
    export let desc: string;
    export let price: number;
    export let image: string;
    export let index: number;

    type itemList = {
        name: string;
        desc: string;
        image: string;
        price: number;
    }[]

    let quant = 1;

    let items = getContext<Writable<itemList>>('iD');
    let globalPrice = getContext<Writable<number>>('gP');
    let globalCount = getContext<Writable<number>>('gC');

    function handleErase(){
        console.log(quant)
        items.set($items.filter((x, i) => i !== index));
        globalPrice.set($globalPrice - (price * quant));
        globalCount.set($globalCount - quant);
    }

    function handleClick(op: number){
        if(op === 0){
            if(quant === 1){
                return;
            }
            quant--;
            globalPrice.set($globalPrice - price)
            globalCount.set($globalCount - 1);
        }
        else if(op === 1){
            quant++;
            globalPrice.set($globalPrice + price)
            globalCount.set($globalCount + 1)
        }
    }

</script>

<style>
    .item-container {
        position: relative;
        width: 14vw;
        background-color: #FAFAFA;
        box-shadow: 0px 0px 6px 2px #ECECEC;
        border-radius: 0.5vw;
    }

    img {
        width: 100%;
        height: 10vw;
        object-fit: cover;
        object-position: 100% 0%;
        border-radius: 0.5vw;
    }

    .info-container {
        display: flex;
        flex-direction: column;
        gap: 1vh;
    }
    
    .quant-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        height: 4vh;
        margin: 4px;
        background-color: #f0f0f0;
        border-radius: 5px;
    }

    button {
        position: absolute;
        right: 0;
        background-color: transparent;
        border: 0;
        color: grey;
    }

    button:hover{
        background-color: #ECECEC;
        cursor: pointer;
    }

    p {
        margin: 2px;
    }

</style>