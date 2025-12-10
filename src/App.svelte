<script>
  import { slide } from "svelte/transition";

  import Stepper from "./lib/components/Stepper.svelte";
  import Otp from "./lib/screens/Otp.svelte";
  import Welcome from "./lib/screens/Welcome.svelte";
  import Background from "./lib/components/Background.svelte";
  import AdultDetails from "./lib/screens/Adult-details.svelte";
  import KidsDetails from "./lib/screens/Kids-details.svelte";
  import Success from "./lib/screens/Success.svelte";
  import Onboard from "./lib/screens/Onboard.svelte";

  let step = 0;
  let adult_data = {};
  let processCompleted = false;
  let restaurant = {};
</script>

<main>
  <div class="wrapper lg:h-screen max-h-screen">
    <div class="wrap flex flex-row h-full">
      <div
        class="card flex flex-col lg:max-w-[70%] max-w-full w-full bg-[#6d8f81] shadow-xl p-8 items-center justify-center"
      >
        {#if step === 0}
          <div in:slide out:slide>
            <Onboard bind:step bind:restaurant />
          </div>
        {/if}

        {#if step > 0}
          <Stepper bind:input={step} />
          {#if step === 1}
            <div in:slide out:slide>
              <Welcome bind:step bind:adult_data />
            </div>
          {/if}
          {#if step === 2}
            <div in:slide out:slide>
              <Otp bind:step bind:adult_data />
            </div>
          {/if}
          {#if step === 3}
            <div class="w-full" in:slide out:slide>
              <AdultDetails bind:step bind:adult_data />
            </div>
          {/if}
          {#if step === 4}
            <div in:slide out:slide>
              <KidsDetails bind:step bind:adult_data />
            </div>
          {/if}
          {#if step === 5}
            <div in:slide out:slide>
              <Success
                bind:processCompleted
                bind:adult_data
                bind:step
                bind:restaurant
              />
            </div>
          {/if}
        {/if}
      </div>

      <div class="flex-1 hidden lg:contents">
        <Background/>
      </div>
    </div>
  </div>
</main>

<style>
  main {

    background-color: #fff;
  }

  .wrapper {
    height: 100vh;
    max-height: 100vh;
  }
  .card {
    border-radius: 0 24px 24px 0;
    width: 100%;
    -webkit-transition: width 1s ease-in-out;
    -moz-transition: width 1s ease-in-out;
    -o-transition: width 1s ease-in-out;
    transition: width 1s ease-in-out;
  }
</style>
