<script lang="ts">
    import { onMount } from "svelte";
    import QR from "@svelte-put/qr/svg/QR.svelte";

    let qrCode: string | null = null;
    async function connectSession() {
        const response = await fetch(
            "https://www.wasenderapi.com/api/whatsapp-sessions/35398/connect",
            {
                method: "POST",
                headers: {
                    Authorization:
                        "Bearer 1008|DS9TJLovDuCCmwHk1UrmJ7wsDvSYKLn8fJ29hqOQ994193ae",
                },
            },
        );
        const result = await response.json();
        return result.data.qrCode;
    }

    onMount(async () => {
        qrCode = await connectSession();
        console.log("QR Code: ", qrCode);
    });
</script>

<div class="wrap">
    {#if qrCode}
        <QR data={qrCode} />
    {/if}
    {#if !qrCode}
        <p>Loading...</p>
    {/if}
</div>

<style>
    .wrap {
        height: 100%;
        width: 100%;

        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
