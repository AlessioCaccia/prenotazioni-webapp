<script lang="ts">
    export let step: number;
    export let adult_data = {};

    import { onMount } from "svelte";

    let counter = 30;
    let enabled = false;
    let interval;

    onMount(async () => {
        await genOtp();

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

    async function genOtp() {
        const otp = Math.floor(1000 + Math.random() * 9000).toString();
        const encoded = btoa(otp); // base64 encode
        localStorage.setItem("otp", encoded);

        const response = await fetch(
            "https://www.wasenderapi.com/api/send-message",
            {
                method: "POST",
                headers: {
                    Authorization:
                        "Bearer 593b836f6ca7b258203371b4a3de98ca3a0d9cfae0981b57ebcbdd21d0536cd2",
                    "Content-Type": "application/json",
                },
                body: JSON.stringify({
                    //@ts-ignore
                    to: adult_data.phone,
                    text:
                        "Ciao, questo è il tuo codice OTP per la verifica telefonica " +
                        otp,
                }),
            },
        );

        const result = await response.json();
        console.log(result);
    }

    function cleanOtp() {
        localStorage.removeItem("otp");
    }

    async function resendCode() {
        if (!enabled) return;
        await genOtp();

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
        const decoded = atob(localStorage.getItem("otp"));

        if (otp.join("") === decoded) {
            cleanOtp();
            step = 3;
        }
    }
</script>

<!-- OTP -->
<div class="w-auto mx-auto mt-6">
    <header class="mb-8">
        <p class="text-[15px] text-white">
            Inserisci il codice di verifica a 4 cifre <br /> che è stato inviato
            al tuo numero di telefono.
        </p>
    </header>
    <form id="otp-form">
        <div class="flex">
            <input
                type="text"
                class="input h-14 text-center text-2xl font-extrabold text-slate-900 bg-slate-100 border border-transparent hover:border-slate-200 appearance-none rounded p-4 outline-none focus:bg-white focus:border-[#3a4943] focus:ring-2 focus:ring-[#3a4943]"
                pattern="\d*"
                maxlength="4"
            />
        </div>
        <div class="mt-4">
            <button
                type="submit"
                class="inline-flex justify-center whitespace-nowrap rounded-lg px-3.5 py-2.5 text-sm font-medium text-white shadow-sm shadow-amber-950/10 bg-[#50685e] hover:bg-[#3a4943] focus:outline-none focus:ring focus:ring-[#3a4943] focus-visible:outline-none focus-visible:ring focus-visible:ring-[#3a4943] transition-colors duration-150"
                on:click|preventDefault={() => handleOtp()}
                >Verifica numero</button
            >
        </div>
    </form>

    <div class="text-sm text-white mt-4">
        Non hai ricevuto il codice? <br />
        {#if !enabled}
            <span class="text-white cursor-pointer">Invia di nuovo fra {counter}s</span>
        {:else}
            <a
                class="font-medium text-mwhite cursor-pointer"
                href="#0"
                on:click|preventDefault={resendCode}>Clicca qui per ricevere un nuovo codice</a
            >
        {/if}
    </div>
</div>
