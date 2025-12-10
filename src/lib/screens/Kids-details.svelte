<script lang="ts">
    import { onMount } from "svelte";

    export let step: number;
    export let adult_data = {} as any;
    let formatted_kids = [];
    let editmode = false;
    let editIndex: number;

    onMount(async () => {
        formatKidsInit();
    });

    function formatKidsInit() {
        if (adult_data.child_count > 0) {
            if (adult_data.child_1_first_name) {
                formatted_kids[0] = {
                    name: adult_data.child_1_first_name,
                    surname: adult_data.child_1_last_name,
                    date: adult_data.child_1_dob,
                    display_date: new Date(
                        adult_data.child_1_dob,
                    ).toLocaleDateString("it-IT"),
                    checked: true,
                };
            }

            if (adult_data.child_2_first_name) {
                formatted_kids[1] = {
                    name: adult_data.child_2_first_name,
                    surname: adult_data.child_2_last_name,
                    date: adult_data.child_1_dob,
                    display_date: new Date(
                        adult_data.child_2_dob,
                    ).toLocaleDateString("it-IT"),
                    checked: true,
                };
            }

            if (adult_data.child_3_first_name) {
                formatted_kids[2] = {
                    name: adult_data.child_3_first_name,
                    surname: adult_data.child_3_last_name,
                    date: adult_data.child_1_dob,
                    display_date: new Date(
                        adult_data.child_3_dob,
                    ).toLocaleDateString("it-IT"),
                    checked: true,
                };
            }

            if (adult_data.child_4_first_name) {
                formatted_kids[3] = {
                    name: adult_data.child_4_first_name,
                    surname: adult_data.child_4_last_name,
                    date: adult_data.child_1_dob,
                    display_date: new Date(
                        adult_data.child_4_dob,
                    ).toLocaleDateString("it-IT"),
                    checked: true,
                };
            }

            if (adult_data.child_5_first_name) {
                formatted_kids[4] = {
                    name: adult_data.child_5_first_name,
                    surname: adult_data.child_5_last_name,
                    date: adult_data.child_1_dob,
                    display_date: new Date(
                        adult_data.child_5_dob,
                    ).toLocaleDateString("it-IT"),
                    checked: true,
                };
            }
        }
    }

    function collectData() {
        Object.assign(adult_data, {
            kids: formatted_kids,
        });

        step = 5;
    }

    function addKid() {
        editmode = true;

        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;

        formatted_kids.push({
            name: name.value,
            surname: surname.value,
            date: date.value,
            display_date: new Date(date.value).toLocaleDateString("it-IT"),
            checked: true,
        });

        editmode = false;
    }

    function enableEdit(index: number) {
        editmode = true;
        editIndex = index;
        if (index != 9) {
            setTimeout(() => {
                //@ts-ignore
                document.getElementById("name").value =
                    formatted_kids[index].name;
                //@ts-ignore
                document.getElementById("surname").value =
                    formatted_kids[index].surname;
                //@ts-ignore
                document.getElementById("date").value =
                    formatted_kids[index].date;
            }, 200);
        }
    }

    function editKid() {
        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;

        formatted_kids[editIndex] = {
            name: name.value,
            surname: surname.value,
            date: date.value,
            display_date: new Date(date.value).toLocaleDateString("it-IT"),
            checked: true,
        };

        editmode = false;
    }

    function removeKid() {
        formatted_kids.splice(editIndex, 1);
        editmode = false;
    }
</script>

<div class="w-auto text-center">
    <h2 class="inter text-white font-light lg:text-5xl text-2xl text-center">
        Dettagli bambini
    </h2>
    <h2 class="text-white font-light lg:text-lg text-sm text-center mt-2">
        Seleziona o registra i bambini del tuo nucleo familiare <br /> per effettuare
        il check-in assicurativo
    </h2>

    {#if formatted_kids.length > 0 && !editmode}
        <div class="grid lg:grid-cols-2 grid-cols-1 w-full mt-8 gap-2">
            {#each formatted_kids as kid, index}
                <div class="flex bg-[#638074] text-left p-3">
                    <div class="flex-1">
                        <h2 class="text-lg uppercase font-light text-white">
                            {kid.name}
                            {kid.surname}
                        </h2>
                        <h2 class="text-s font-light text-white">
                            {kid.display_date}
                        </h2>
                    </div>
                    <div class="flex flex-col gap-2">
                        <input
                            type="checkbox"
                            bind:checked={kid.checked}
                            class="checkbox"
                        />

                        <button
                            class="btn btn-square btn-xs"
                            on:click|preventDefault={() => enableEdit(index)}
                        >
                            <svg
                                width="18"
                                height="18"
                                viewBox="0 0 48 48"
                                class="size-5"
                                fill="none"
                                xmlns="http://www.w3.org/2000/svg"
                                ><path
                                    d="M7 42H43"
                                    stroke="white"
                                    stroke-width="3"
                                    stroke-linecap="butt"
                                    stroke-linejoin="bevel"
                                ></path><path
                                    d="M11 26.7199V34H18.3172L39 13.3081L31.6951 6L11 26.7199Z"
                                    fill="none"
                                    stroke="white"
                                    stroke-width="3"
                                    stroke-linejoin="bevel"
                                ></path></svg
                            >
                        </button>
                    </div>
                </div>
            {/each}
        </div>
    {:else if editmode}
        <div
            class="lg:grid lg:grid-cols-2 gap-x-6 gap-y-2 lg:mt-8 justify-items-center"
        >
            <fieldset class="fieldset w-full">
                <legend
                    class="fieldset-legend lg:text-xl text-lg text-white font-light"
                    >Nome</legend
                >
                <input
                    id="name"
                    type="text"
                    class="input lg:input-lg input-sm w-full"
                />
            </fieldset>

            <fieldset class="fieldset w-full">
                <legend
                    class="fieldset-legend lg:text-xl text-lg text-white font-light"
                    >Cognome</legend
                >
                <input
                    id="surname"
                    type="text"
                    class="input lg:input-lg input-sm w-full"
                />
            </fieldset>

            <fieldset class="fieldset w-full">
                <legend
                    class="fieldset-legend lg:text-xl text-lg text-white font-light"
                    >Data di nascita</legend
                >
                <input
                    id="date"
                    type="date"
                    class="input lg:input-lg input-sm w-full"
                />
            </fieldset>
        </div>
    {/if}

    <div class="flex items-center justify-center gap-x-4 lg:mt-10 mt-4">
        {#if editmode && editIndex != 9}
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => removeKid()}
                >Elimina bimbo</button
            >
        {/if}
        {#if editmode && editIndex != 9}
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => editKid()}
                >Salva modifiche</button
            >
        {/if}
        {#if !editmode && formatted_kids.length < 5}
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => enableEdit(9)}
                >Aggiungi bimbo</button
            >
        {/if}
        {#if editmode && formatted_kids.length < 5 && editIndex == 9}
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => (editmode = false)}
                >Annulla</button
            >
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => addKid()}>Salva</button
            >
        {/if}
        {#if !editmode}
            <button
                class="btn lg:btn-lg btn-md"
                on:click|preventDefault={() => collectData()}>Continua</button
            >
        {/if}
    </div>

    <h2
        class="text-white font-light lg:text-md text-sm text-center lg:mt-20 mt-8"
    >
        IMPORTANTE: associa esclusivamente i bambini del tuo nucleo familiare
        per garantire la corretta PROTEZIONE assicurativa.
    </h2>
</div>
