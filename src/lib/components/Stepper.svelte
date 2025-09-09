<script lang="ts">
    export let input: number;
</script>

<!-- STEPS -->
<div class="absolute top-6 mx-auto">
    <ul class="steps">
        {#each Array(4) as _, i}
            <li class="step {input >= i+1 ? 'step-primary' : ''}">
            <!-- <button on:click={() => input = i+1} class="px-2 py-1">{i+1}</button> -->
            </li>
        {/each}
    </ul>
</div>

<style> 
    .step::after {
        border-radius: 7px;
    }
</style>
