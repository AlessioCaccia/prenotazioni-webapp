<script>
  import { slide } from "svelte/transition";

  import Stepper from "./lib/components/Stepper.svelte";
  import Otp from "./lib/screens/Otp.svelte";
  import Welcome from "./lib/screens/Welcome.svelte";
  import Background from "./lib/components/Background.svelte";
  import AdultDetails from "./lib/screens/Adult-details.svelte";
  import KidsDetails from "./lib/screens/Kids-details.svelte";
  import Success from "./lib/screens/Success.svelte";

  let step = 1;
  let data = {};
  let processCompleted = false;

</script>

<main>
  <div class="wrapper">
    <div class="wrap flex flex-row h-full">
      <div
        class="card flex flex-col w-full bg-white shadow-xl p-8 items-center justify-center"
      >
        <Stepper bind:input={step} />
        {#if step === 1}
          <div in:slide out:slide>
            <Welcome bind:step bind:data />
          </div>
        {/if}
        {#if step === 2}
          <div in:slide out:slide>
            <Otp bind:step bind:data />
          </div>
        {/if}
        {#if step === 3}
          <div in:slide out:slide>
            <AdultDetails bind:step bind:data />
          </div>
        {/if}
        {#if step === 4}
          <div in:slide out:slide>
            <KidsDetails bind:step bind:data />
          </div>
        {/if}
        {#if step === 5}
          <div in:slide out:slide>
            <Success bind:processCompleted bind:data bind:step/>
          </div>
        {/if}
      </div>

      <div class="flex-1">
        <Background bind:input={step} />
      </div>
    </div>
  </div>
</main>

<style>
  main {
    background-color: #feece4;
  }
  .wrapper {
    height: 100vh;
    max-height: 100vh;
  }
  .card {
    border-radius: 0 24px 24px 0;

    max-width: 700px;
    width: 100%;
    -webkit-transition: width 1s ease-in-out;
    -moz-transition: width 1s ease-in-out;
    -o-transition: width 1s ease-in-out;
    transition: width 1s ease-in-out;
  }
</style>
