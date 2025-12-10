<script lang="ts">
    import { createClient } from "@supabase/supabase-js";
    import { onMount } from "svelte";

    export let step: number;
    export let adult_data = {} as any;

    let getStoredClientData = false;

    onMount(async () => {
        if (!getStoredClientData) {
            await getClientData();
        }
    });

    async function getClientData() {
        const supabase = createClient(
            "https://clgdfcnrmktvhicgtgnt.supabase.co",
            "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImNsZ2RmY25ybWt0dmhpY2d0Z250Iiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc1OTkwMDQ1NywiZXhwIjoyMDc1NDc2NDU3fQ.b_4kV6jMFa7LOOOx5YWA5m05QSTJ_WnT4DEdjjBb_5g",
        );

        const { data, error } = await supabase
            .from("benvenuto db - 13.10.25")
            .select("*")
            .eq("adult_phone", adult_data.phone);

        if (data) {
            Object.assign(adult_data, data[0]);

            //@ts-ignore
            document.getElementById("name").value = adult_data.adult_first_name;
            //@ts-ignore
            document.getElementById("surname").value =
                adult_data.adult_last_name;
            //@ts-ignore
            // document.getElementById("gender").value =
            //     adult_data.adult_gender;
            //@ts-ignore
            document.getElementById("date").value = adult_data.adult_dob;
            //@ts-ignore
            document.getElementById("email").value = adult_data.adult_email;
            //@ts-ignore
            document.getElementById("cap").value = adult_data.cap;
        }

        getStoredClientData = true;
    }

    function collectData() {
        const name = document.getElementById("name") as HTMLInputElement;
        const surname = document.getElementById("surname") as HTMLInputElement;
        // const gender = document.getElementById("gender") as HTMLInputElement;
        const date = document.getElementById("date") as HTMLInputElement;
        const email = document.getElementById("email") as HTMLInputElement;
        const cap = document.getElementById("cap") as HTMLInputElement;
        const table = document.getElementById("table") as HTMLInputElement;

        if(table.value == "") {
            alert(`Il campo tavolo è richiesto`);
            return false;
        }
        


        Object.assign(adult_data, {
            name: name.value,
            surname: surname.value,
            // gender: gender.value,
            date: date.value,
            email: email.value,
            cap: cap.value,
            table: table.value,
        });

        step = 4;
    }
</script>

<div class="w-auto mx-auto {!getStoredClientData ? 'block' : 'hidden'}">
    <h2 class="text-white inter font-light text-2xl text-center">
        Attendi un momento <span class="loading loading-dots loading-sm"></span>
    </h2>
</div>

<div
    class="w-auto text-center lg:mt-0 mt-10 {!getStoredClientData
        ? 'hidden'
        : 'block'}"
>
    <h2 class="text-white inter font-light lg:text-5xl text-2xl">
        Dettagli adulto
    </h2>

    <div
        class="lg:grid lg:grid-cols-2 gap-x-6 gap-y-2 lg:mt-8 justify-items-cente"
    >
        <fieldset class="fieldset w-full col-span-2">
            <legend
                class="fieldset-legend lg:text-xl text-lg text-white font-light"
                >Email</legend
            >
            <input
                id="email"
                type="email"
                class="input lg:input-lg input-sm w-full"
            />
        </fieldset>

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
        <!-- 
            <fieldset class="fieldset w-full">
                <legend
                    class="fieldset-legend lg:text-xl text-lg text-white font-light"
                    >Genere</legend
                >
                <select
                    id="gender"
                    class="select lg:select-lg select-sm w-full"
                >
                    <option disabled selected>Seleziona un genere</option>
                    <option>Femmina</option>
                    <option>Maschio</option>
                </select>
            </fieldset> -->

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

        <fieldset class="fieldset w-full">
            <legend
                class="fieldset-legend lg:text-xl text-lg text-white font-light"
                >CAP</legend
            >
            <input
                id="cap"
                type="number"
                class="input lg:input-lg input-sm w-full"
            />
        </fieldset>

        <fieldset class="fieldset w-full">
            <legend
                class="fieldset-legend lg:text-xl text-lg text-white font-light"
                >Numero tavolo
            </legend>
            <input
                id="table"
                type="number"
                class="input lg:input-lg input-sm w-full"
            />
        </fieldset>
    </div>

    <button
        class="btn lg:btn-lg btn-md lg:mt-10 mt-4 text-white"
        on:click|preventDefault={() => collectData()}>Continua</button
    >
</div>
