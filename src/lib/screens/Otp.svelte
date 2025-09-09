<script lang="ts">
    export let step: number;
    export let data = {};

    import { onMount } from "svelte";
    let counter = 30;
    let enabled = false;
    let interval;

    onMount(() => {
        interval = setInterval(() => {
            if (counter > 0) {
                counter -= 1;
            }
            if (counter === 0) {
                enabled = true;
                clearInterval(interval);
            }
        }, 1000);
    });

    function resendCode() {
        if (!enabled) return;
        // Add resend logic here
        counter = 30;
        enabled = false;
        interval = setInterval(() => {
            if (counter > 0) {
                counter -= 1;
            }
            if (counter === 0) {
                enabled = true;
                clearInterval(interval);
            }
        }, 1000);
    }

    function handleOtp() {
        const inputs = document.querySelectorAll('input[type="text"]');
        //@ts-ignore
        const otp = Array.from(inputs).map((input) => input.value);
        
        if (otp.join("") === "1234") {
            step = 3;
        }
    }
</script>

<!-- OTP -->
<div class="w-auto mx-auto text-center mt-6">
    <header class="mb-8">
        <p class="text-[15px] text-slate-500">
            Inserisci il codice di verifica a 4 cifre <br /> che è stato inviato
            al tuo numero di telefono.
        </p>
    </header>
    <form id="otp-form">
        <div class="flex items-center justify-center gap-3">
            <input
                type="text"
                class="w-14 h-14 text-center text-2xl font-extrabold text-slate-900 bg-slate-100 border border-transparent hover:border-slate-200 appearance-none rounded p-4 outline-none focus:bg-white focus:border-amber-900 focus:ring-2 focus:ring-amber-800"
                pattern="\d*"
                maxlength="1"
            />
            <input
                type="text"
                class="w-14 h-14 text-center text-2xl font-extrabold text-slate-900 bg-slate-100 border border-transparent hover:border-slate-200 appearance-none rounded p-4 outline-none focus:bg-white focus:border-amber-900 focus:ring-2 focus:ring-amber-800"
                maxlength="1"
            />
            <input
                type="text"
                class="w-14 h-14 text-center text-2xl font-extrabold text-slate-900 bg-slate-100 border border-transparent hover:border-slate-200 appearance-none rounded p-4 outline-none focus:bg-white focus:border-amber-900 focus:ring-2 focus:ring-amber-800"
                maxlength="1"
            />
            <input
                type="text"
                class="w-14 h-14 text-center text-2xl font-extrabold text-slate-900 bg-slate-100 border border-transparent hover:border-slate-200 appearance-none rounded p-4 outline-none focus:bg-white focus:border-amber-900 focus:ring-2 focus:ring-amber-800"
                maxlength="1"
            />
        </div>
        <div class="max-w-[260px] mx-auto mt-4">
            <button
                type="submit"
                class="w-full inline-flex justify-center whitespace-nowrap rounded-lg bg-amber-900 px-3.5 py-2.5 text-sm font-medium text-white shadow-sm shadow-amber-950/10 hover:bg-amber-800 focus:outline-none focus:ring focus:ring-amber-800 focus-visible:outline-none focus-visible:ring focus-visible:ring-amber-800 transition-colors duration-150"
                on:click|preventDefault={() => handleOtp()}>Verifica numero</button
            >
        </div>
    </form>

    <div class="text-sm text-slate-500 mt-4">
        Non hai ricevuto il codice? <br />
        {#if !enabled}
            <span class="ml-2 text-amber-900">Invia di nuovo ({counter}s)</span>
        {:else}
            <a
                class="font-medium text-amber-900 hover:text-amber-600 ml-2 cursor-pointer"
                href="#0"
                on:click|preventDefault={resendCode}>Invia di nuovo</a
            >
        {/if}
    </div>
</div>
