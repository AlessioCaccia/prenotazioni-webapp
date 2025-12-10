<script lang="ts">
    import { onMount } from "svelte";

    export let step: number;
    export let restaurant = {};

    onMount(async () => {
        if (window.location.search) {
            let search =
                window.location.search
                    .replace(/^\?/, "")
                    .charAt(0)
                    .toUpperCase() +
                window.location.search
                    .replace(/^\?/, "")
                    .slice(1)
                    .toLowerCase();

            collectData(search);
        }
    });

    function collectData(data: string) {
        switch (data) {
            case "Torino":
                Object.assign(restaurant, {
                    name: "Torino",
                    address: "Via Caraglio 97, Torino",
                    phone: "+39 011 016 00 59",
                    phone2: "+39 327 732 14 90",
                    mail: "torino_webapp@food-fun.it",
                });
                break;
            case "Milano":
                Object.assign(restaurant, {
                    name: "Milano",
                    address: "Via Fernanda Wittengs 6/B, Milano",
                    phone: "+39 02 841 00 698",
                    phone2: "+39 351 88 57 882",
                    mail: "milano_webapp@food-fun.it",
                });
                break;
            case "Venaria":
                Object.assign(restaurant, {
                    name: "Venaria",
                    address: "C.so Garibaldi 155, Venaria",
                    phone: "+39 011 197.15.073",
                    phone2: "+39 320 44 70 812",
                    mail: "venaria_webapp@food-fun.it",
                });
                break;
            case "Monza":
                Object.assign(restaurant, {
                    name: "Monza",
                    address: "Via Solferino 29/A, Monza",
                    phone: "+39 039 636 1032",
                    phone2: "+39 344 349 0652",
                    mail: "monza_webapp@food-fun.it",
                });
                break;
        }

        if (
            data == "Torino" ||
            data == "Monza" ||
            data == "Milano" ||
            data == "Venaria"
        ) {
            step = 1;
        }
    }
</script>

<div class="flex flex-col gap-8">
    <h2 class="text-white inter font-light text-5xl mb-8">
        Seleziona il tuo ristorante
    </h2>

    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Torino")}>Torino</button
    >
    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Milano")}>Milano</button
    >
    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Venaria")}>Venaria</button
    >
    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Monza")}>Monza</button
    >
</div>
