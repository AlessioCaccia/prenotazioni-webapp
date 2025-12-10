<script lang="ts">
    import { onMount } from "svelte";
    import { jsPDF } from "jspdf";
    import { createClient } from "@supabase/supabase-js";

    export let adult_data = {} as any;
    export let restaurant = {} as any;
    export let processCompleted;
    export let step: number;

    onMount(async () => {
        if (step === 5) {
            await sendData().then(() => {
                processCompleted = true;
                Object.assign(processCompleted, true);
            });
        }
    });

    async function createAndSendPDF() {
        // Convert mm to jsPDF units (by default 'mm' = 1:1)
        const pageWidth = 81.3;
        const pageHeight = 84.6;

        // Initialize the PDF with custom page size
        const doc = new jsPDF({
            orientation: "portrait",
            unit: "mm",
            format: [pageWidth, pageHeight],
        });

        adult_data.kids.filter((item) => item.checked === true).forEach((kidDetails, index) => {
            if (index > 0) doc.addPage([pageWidth, pageHeight]); // new page

            const text = `${kidDetails.name}\n\n Tavolo ${adult_data.table}`;

            // Font styling
            doc.setFont("helvetica", "normal");
            doc.setFontSize(30);

            // Split into lines (so it centers multiline text correctly)
            const lines = text.split("\n");

            // Measure the width and height of the text block
            const lineHeight = 8; // roughly 8mm per line at fontSize 16
            const textBlockHeight = lines.length * lineHeight;

            // Compute vertical starting position
            const startY = (pageHeight - textBlockHeight) / 2 + lineHeight / 2;

            // Draw each line centered horizontally
            lines.forEach((line, i) => {
                const textWidth = doc.getTextWidth(line);
                const x = (pageWidth - textWidth) / 2;
                const y = startY + i * lineHeight;
                doc.text(line, x, y);
            });
        });

        // 2. Convert to Blob
        const pdfBlob = doc.output("blob");
        const formData = new FormData();

        const now = new Date();
        const timestamp = now.toISOString().replace(/[:.-]/g, "");
        // Example result: "20251111T093812123Z"
        const fileName = `children-${timestamp}.pdf`;

        // 3. Append form fields
        formData.append("action", "send_custom_email");
        formData.append("email", restaurant.mail);
        formData.append("subject", "New Customer");
        formData.append("message", "Customer");
        formData.append("attachment", pdfBlob, fileName);

        // 4. Send to your WordPress custom endpoint
        const res = await fetch(
            "https://www.food-fun.it/wp-admin/admin-ajax.php",
            {
                method: "POST",
                body: formData,
            },
        );

        return res;
    }

    async function sendToDb() {
        const supabase = createClient(
            "https://clgdfcnrmktvhicgtgnt.supabase.co",
            "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImNsZ2RmY25ybWt0dmhpY2d0Z250Iiwicm9sZSI6InNlcnZpY2Vfcm9sZSIsImlhdCI6MTc1OTkwMDQ1NywiZXhwIjoyMDc1NDc2NDU3fQ.b_4kV6jMFa7LOOOx5YWA5m05QSTJ_WnT4DEdjjBb_5g",
        );

        const { data, error } = await supabase
            .from("benvenuto db - 13.10.25")
            .upsert([
                {
                    id: adult_data.id,
                    adult_first_name: adult_data.name,
                    adult_last_name: adult_data.surname,
                    adult_phone: adult_data.phone,
                    adult_email: adult_data.email,
                    adult_dob: adult_data.date,
                    child_count: adult_data.kids.length,
                    sede: restaurant.name,
                    cap: adult_data.cap,
                    child_1_first_name: adult_data.kids[0]
                        ? adult_data.kids[0].name
                        : null,
                    child_1_last_name: adult_data.kids[0]
                        ? adult_data.kids[0].surname
                        : null,
                    child_1_dob: adult_data.kids[0]
                        ? adult_data.kids[0].date
                        : null,

                    child_2_first_name: adult_data.kids[1]
                        ? adult_data.kids[1].name
                        : null,
                    child_2_last_name: adult_data.kids[1]
                        ? adult_data.kids[1].surname
                        : null,
                    child_2_dob: adult_data.kids[1]
                        ? adult_data.kids[1].date
                        : null,

                    child_3_first_name: adult_data.kids[2]
                        ? adult_data.kids[2].name
                        : null,
                    child_3_last_name: adult_data.kids[2]
                        ? adult_data.kids[2].surname
                        : null,
                    child_3_dob: adult_data.kids[2]
                        ? adult_data.kids[2].date
                        : null,

                    child_4_first_name: adult_data.kids[3]
                        ? adult_data.kids[3].name
                        : null,
                    child_4_last_name: adult_data.kids[3]
                        ? adult_data.kids[3].surname
                        : null,
                    child_4_dob: adult_data.kids[3]
                        ? adult_data.kids[3].date
                        : null,

                    child_5_first_name: adult_data.kids[4]
                        ? adult_data.kids[4].name
                        : null,
                    child_5_last_name: adult_data.kids[4]
                        ? adult_data.kids[4].surname
                        : null,
                    child_5_dob: adult_data.kids[4]
                        ? adult_data.kids[4].date
                        : null,
                },
            ])
            .select();
    }

    async function sendData() {
        await sendToDb();
        await createAndSendPDF();
    }
</script>

{#if !processCompleted}
    <div class="w-auto">
        <h2 class="text-white inter font-light text-2xl">
            Attendi un momento <span class="loading loading-dots loading-sm"
            ></span>
        </h2>
    </div>
{:else}
    <!-- TESTO -->
    <div class="w-auto">
        <h2 class="text-white inter font-light text-5xl">
            Procedura completata
        </h2>
        <h2 class="text-white font-light text-lg mt-4">
            Hai completato con successo la procedura di prenotazione. <br /> Ti
            ringraziamo per aver scelto di utilizzare il nostro servizio.
            <!-- Riceverai un'email con le informazioni relative alla tua prenotazione. -->
        </h2>

        <h2 class="text-white inter font-light text-lg mt-8">
            Il tuo ristorante si trova a:
        </h2>
        <h2 class="text-white inter font-light text-3xl mt-3">
            {restaurant.name}
        </h2>
        <h2 class="text-white inter font-light text-xl mt-1">
            {restaurant.address}
        </h2>
        <h2 class="text-white inter font-light text-xl mt-1">
            {restaurant.phone}
        </h2>
        <h2 class="text-white inter font-light text-xl mt-1">
            {restaurant.phone2}
        </h2>
    </div>
{/if}

<style>
</style>
