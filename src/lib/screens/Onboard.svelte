<script lang="ts">
    export let step: number;
    export const restaurant = {};

    function collectData(restaurant: string) {
        switch (restaurant) {
            case "Torino":
                Object.assign(restaurant, {
                    name: "Torino",
                    address: "Via Torino, 1",
                    phone: "333333333",
                    mail: "torino_webapp@benvenuto.org",
                });
                break;
            case "Verona":
                Object.assign(restaurant, {
                    name: "Verona",
                    address: "Via Verona, 1",
                    phone: "333333333",
                    mail: "verona_webapp@benvenuto.org",
                });
                break;
            case "Milano":
                Object.assign(restaurant, {
                    name: "Milano",
                    address: "Via Milano, 1",
                    phone: "333333333",
                    mail: "milanovetra_webapp@benvenuto.org",
                });
                break;
            case "Venaria":
                Object.assign(restaurant, {
                    name: "Venaria",
                    address: "Via Venaria, 1",
                    phone: "333333333",
                    mail: "venaria_webapp@benvenuto.org",
                });
                break;
            case "Monza":
                Object.assign(restaurant, {
                    name: "Monza",
                    address: "Via Monza, 1",
                    phone: "333333333",
                    mail: "monza_webapp@benvenuto.org",
                });
                break;
            case "Rivalta":
                Object.assign(restaurant, {
                    name: "Rivalta",
                    address: "Via Rivalta, 1",
                    phone: "333333333",
                    mail: "rivalta1_webapp@benvenuto.org",
                    // mail: "rivalta2_webapp@benvenuto.org",
                });
                break;
        }

        step = 1;
    }
</script>

<div class="flex flex-col gap-8">
    <h2 class="text-gray-900 inter font-semibold text-5xl text-center mb-8">
        Seleziona il tuo ristorante
    </h2>

    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Torino")}>Torino</button
    >
    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Verona")}>Verona</button
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
    <button
        class="btn btn-xl"
        on:click|preventDefault={() => collectData("Rivalta")}>Rivalta</button
    >
</div>
