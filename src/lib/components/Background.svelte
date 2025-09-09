<script lang="ts">
    import family_bg from "../../assets/1.png";
    import otp_bg from "../../assets/2.png";
    import detal_bg from "../../assets/3.png";
    import kids_bg from "../../assets/4.png";

    import { blur } from "svelte/transition";

    export let input: number;
</script>

<div class="w-full h-full overflow-hidden m-auto">
    {#if input === 1}
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
    {/if}
</div>
