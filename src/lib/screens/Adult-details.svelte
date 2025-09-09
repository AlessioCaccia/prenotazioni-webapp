<script lang="ts">
    export let step: number;
    export let data = {};

    function collectData() {
        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        const gender = document.getElementById("gender") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;
        const email = document.getElementById("email") as HTMLInputElement;
        const cap = document.getElementById("cap") as HTMLInputElement;
        const table = document.getElementById("table") as HTMLInputElement;

        Object.assign(data, {
            name: name.value,
            surname: surname.value,
            gender: gender.value,
            date: date.value,
            email: email.value,
            cap: cap.value,
            table: table.value,
        });

        step = 4;
    }
</script>

<div class="w-auto text-center">
    <h2 class="text-gray-900 inter font-semibold text-5xl text-center">
        Dettagli adulto
    </h2>
    <h2 class="text-gray-700 text-m text-center invisible">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod
        tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
        veniam
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

        <fieldset class="fieldset w-full col-span-2">
            <legend class="fieldset-legend text-xl font-medium">Email</legend>
            <input id="email" type="email" class="input input-l w-full" />
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium">CAP</legend>
            <input id="cap" type="number" class="input input-l w-full" />
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend class="fieldset-legend text-xl font-medium"
                >Numero tavolo
            </legend>
            <input id="table" type="number" class="input input-l w-full" />
        </fieldset>
    </div>

    <button
        class="btn btn-lg mt-10 bg-amber-900 text-white"
        on:click|preventDefault={() => collectData()}>Continua</button
    >
</div>
