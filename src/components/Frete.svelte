<form on:submit|preventDefault={() => handleSubmit(cep)}>
    <label>
        <strong>CEP:</strong>
        <input bind:value={cep} type="text" placeholder='Insira um CEP válido.' pattern="[0-9]&#123;5&#125;[\-]?[0-9]&#123;3&#125;" required>
        <input type="submit" value="Calcular">
    </label>
    <p>{information}</p>
</form>

<script lang="ts">
    import { getContext } from 'svelte';
    import { api } from '../services/api';
    import type { Writable } from 'svelte/store';

    let cep: string;
    let information: string = '';
    let freteData: any;
    let globalFrete = getContext<Writable<number>>('gF');

    async function handleSubmit(cep: string){
        try{
        const response = await api.get(`${cep}/json`)
        freteData = response.data
        console.log(freteData)
    }

    catch{
        cep = '';
        information = 'Erro ao verificar o CEP informado.';
        return;
    }

    if(freteData.erro === true){
        globalFrete.set(0);
        cep = '';
        information = 'Erro ao verificar o CEP informado.';
    }

    else if(freteData.uf === "RN" || freteData.uf === "CE" || freteData.uf === "PE" || freteData.uf === "MA" || freteData.uf === "SE" || freteData.uf === "PI" || freteData.uf === "PB" || freteData.uf === "BA"){
        globalFrete.set(0);
        cep = '';
        information = freteData.localidade + ' - ' + freteData.uf;
        return;
    }
    else if(freteData.uf == "RR" || freteData.uf === "RO" || freteData.uf === "PA" || freteData.uf === "AC" || freteData.uf === "PA" || freteData.uf === "AP" || freteData.uf === "MT"){
        globalFrete.set(50);
        cep = '';
        information = freteData.localidade + ' - ' + freteData.uf;
        return
    }
    else{
        globalFrete.set(35);
        cep = '';
        information = freteData.localidade + ' - ' + freteData.uf;
        return
    }
    }
</script>

<style>
    label {
        display: flex;
        gap: 1vw;
    }
</style>