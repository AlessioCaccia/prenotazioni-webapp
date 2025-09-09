<!-- STEP 3/3: Dettagli Bambini Seleziona o registra i bambini del tuo nucleo
familiare per effettuare il check-in assicurativo. IMPORTANTE: associa
esclusivamente i bambini del tuo nucleo familiare per garantire la corretta
PROTEZIONE assicurativa. Nome Cognome Genere Select... Data di Nascita Consenso
al trattamento dei dati personali (Privacy Policy)(Cookie Policy) e per usi
commerciali -->

<script lang="ts">
    export let step: number;
    export let data = {};

    function collectData() {
        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        const gender = document.getElementById("gender") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;

        Object.assign(data, {
            kids: {
                name: name.value,
                surname: surname.value,
                gender: gender.value,
                date: date.value,
            },
        });

        console.log(data);

        step = 5;
    }

    function addKid() {
        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        const gender = document.getElementById("gender") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;

        name.value = "";
        surname.value = "";
        gender.value = "";
        date.value = "";
    }
</script>

<div class="w-auto text-center">
    <h2 class="text-gray-900 inter font-semibold text-5xl text-center">
        Dettagli bambini
    </h2>
    <h2 class="text-gray-700 text-lg text-center mt-2">
        Seleziona o registra i bambini del tuo nucleo familiare <br /> per effettuare
        il check-in assicurativo.
    </h2>

    <div class="grid grid-cols-2 gap-x-6 gap-y-2 mt-8 justify-items-center">
        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium">Nome</legend>
            <input id="name" type="text" class="input input-l w-full" />
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium">Cognome</legend>
            <input id="surname" type="text" class="input input-l w-full" />
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium">Genere</legend>
            <select id="gender" class="select select-l w-full">
                <option disabled selected>Seleziona un genere</option>
                <option>Femmina</option>
                <option>Maschio</option>
            </select>
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium"
                >Data di nascita</legend
            >
            <input id="date" type="date" class="input input-l w-full" />
        </fieldset>
    </div>

    <div class="flex items-center justify-center gap-x-4 mt-10">
        <button
            class="btn btn-lg bg-gray-200 text-gray-700"
            on:click|preventDefault={() => addKid()}>Aggiungi altro</button
        >
        <button
            class="btn btn-lg bg-amber-900 text-white"
            on:click|preventDefault={() => collectData()}>Continua</button
        >
    </div>

    <h2 class="text-gray-700 text-m text-center mt-20">
        IMPORTANTE: associa esclusivamente i bambini del tuo nucleo familiare
        per garantire la corretta PROTEZIONE assicurativa.
    </h2>
</div>
