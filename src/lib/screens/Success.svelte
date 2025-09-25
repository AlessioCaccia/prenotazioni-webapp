<script lang="ts">
    export let data = {};
    export let processCompleted;
    export let step: number;

    import { onMount } from "svelte";

    onMount(async () => {
        if (step === 5) {
            await sendData();
        }
    });

    async function sendData() {
        // todo svuotare localhost
    }
</script>

<!-- TESTO -->
<div class="w-auto">
    <h2 class="text-gray-900 inter font-semibold text-5xl text-center">
        Procedura completata
    </h2>
    <h2 class="text-gray-700 text-lg text-center mt-2">
        Hai completato con successo la procedura di prenotazione. Ti ringraziamo
        per aver scelto di utilizzare il nostro servizio.
        <!-- Riceverai un'email con le informazioni relative alla tua prenotazione. -->
    </h2>
</div>

<style>
</style>
