<script lang="ts">
  import Title from "./components/Title.svelte";
  import Item from "./components/Item.svelte";
  import { itemData } from "./assets/Items"
  import { writable } from "svelte/store";
  import { setContext } from "svelte";
  import Frete from "./components/Frete.svelte";
  import Resumo from "./components/Resumo.svelte";

  let titulo = "Carrinho de Compras";
  let desc = "Esses são os itens adicionados ao carrinho:";
  
  let items = writable(itemData);
  setContext('iD', items);
  let globalCount = writable(5)
  setContext('gC', globalCount);
  let globalPrice = writable(27650)
  setContext('gP', globalPrice);
  let globalFrete = writable(0)
  setContext('gF', globalFrete);

</script>

<main>
  <Title {titulo} {desc}/>
  <p>Você tem {$globalCount} {$globalCount === 1 ? 'item' : 'items'} no carrinho.</p>
  <div class="cart-container">
    <div class="item-list">
      {#if $globalCount === 0}
      <h1>Carrinho vazio.</h1>
      {/if}
      {#each $items as item, i (item.name)}
        <Item nome={item.name} desc={item.desc} image={item.image} price={item.price} index={i}/>
      {/each}
    </div>
    <div class="info-container">
      <Resumo/>
    </div>
  </div>
</main>

<style>
  .cart-container {
    display: flex;
    justify-content: space-between;
  }

  .item-list {
    background-color: #FAFAFA;
    width: 60vw;
    display: flex;
    flex-wrap: wrap;
    gap: 1vw;

  }

  .info-container {
    background-color: #FAFAFA;
    
    box-shadow: 0px 0px 6px 2px #ECECEC;
    width: 35vw;
    border-radius: 0.5vw;
  }
</style>