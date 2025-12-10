<script lang="ts">
    import logo from "../../assets/logo.png";

    import { blur } from "svelte/transition";

    // export let input: number;
</script>

<div class="w-full h-full flex items-center justify-center overflow-hidden m-auto">
    <img
        class="object-contain bg-center"
        src={logo}
        alt="Details"
        in:blur={{ duration: 800 }}
    />
    <!-- {#if input === 1}
        <img
            class="object-cover bg-center w-full h-full"
            src={family_bg}
            alt="Family"
            in:blur={{ duration: 800 }}
        />
    {:else if input === 2}
        <img
            class="object-contain bg-center h-full w-full"
            src={otp_bg}
            alt="OTP"
            in:blur={{ duration: 800 }}
        />
    {:else if input === 3}
        <img
            class="object-contain bg-center w-full h-full"
            src={detal_bg}
            alt="Details"
            in:blur={{ duration: 800 }}
        />
    {:else if input === 4}
        <img
            class="object-cover bg-center w-full h-full"
            src={kids_bg}
            alt="Details"
            in:blur={{ duration: 800 }}
        />
    {/if} -->
</div>
