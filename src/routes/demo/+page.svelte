<script>
    export const ssr = true;
    export const csr = false;

    let img = null;
    let error = null;
    let loading = false;
    let prediction = null;

    async function handleFile(event) {
        if (event.target.files.length === 0) {
            return;
        }

        error = null;
        prediction = null;
        loading = true;

        img = URL.createObjectURL(event.target.files[0]);

        const form = new FormData();
        form.append('file', event.target.files[0]);

        const res = await fetch('https://aidetector-api.pkasila.net/detect', {
            method: 'POST',
            body: form
        });

        if (res.status !== 200) {
            error = res.statusText;
            loading = false;
            return;
        }

        prediction = (await res.json()).prediction;
        loading = false;
    }
</script>

<svelte:head>
    <title>Дэманстрацыя</title>
</svelte:head>

<div class="flex flex-col space-y-4 px-2 md:flex-row md:space-x-4 md:space-y-0 md:items-start md:py-8 items-center justify-center">
    <div class="w-full h-fit md:w-96 rounded-lg flex items-center justify-center border-2 border-gray-300 bg-gray-50
     dark:border-gray-700 dark:bg-gray-800 dark:text-gray-400 shadow-lg overflow-hidden">
        {#if img != null}
            <img src={img} class="w-full h-full object-contain bg-gray-900" alt="Ваша выява"/>
        {:else}
            <p class="py-8 md:py-0 md:h-96 md:flex md:items-center md:justify-center">
                Абярыце выяву
            </p>
        {/if}
    </div>
    <div class="w-full md:w-96 h-fit rounded-lg flex flex-col space-y-4 items-center justify-start border bg-white shadow-lg p-4
                dark:border-gray-700 dark:bg-gray-800 dark:text-gray-200">
        <div class="flex flex-col w-full">
            <label class="block mb-2 text-sm font-medium" for="file_input">Абраць
                выяву</label>
            <input class="block w-full text-sm text-gray-900 border border-gray-300 rounded-lg cursor-pointer file:cursor-pointer bg-gray-50 focus:outline-none
file:bg-gray-700 file:text-gray-200 file:border-0 file:rounded-l-lg file:px-2 file:py-1.5 hover:file:bg-gray-900 file:transition-colors file:ease-in-out
dark:border-gray-700 dark:text-gray-200 dark:bg-gray-800 dark:hover:file:bg-gray-600"
                   aria-describedby="file_input_help" id="file_input" type="file" on:change={handleFile}
                   accept="image/*">
            <p class="mt-1 text-sm text-gray-500 dark:text-gray-300" id="file_input_help">Лепш грузіць JPEG ці PNG</p>
        </div>

        {#if loading}
            <div role="status">
                <svg aria-hidden="true"
                     class="inline w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-gray-600 dark:fill-gray-300"
                     viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                          fill="currentColor"/>
                    <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                          fill="currentFill"/>
                </svg>
                <span class="sr-only">Loading...</span>
            </div>
        {/if}

        {#if error != null}
            <div class="p-4 mb-4 text-sm text-red-800 rounded-lg bg-red-50 dark:bg-gray-800 dark:text-red-400"
                 role="alert">
                <span class="font-medium">Памылка!</span> {error}
            </div>
        {/if}

        {#if prediction != null}
            <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                <tr>
                    <th scope="col" class="px-3 py-1.5">
                        Метка
                    </th>
                    <th scope="col" class="px-3 py-1.5">
                        Значэнне
                    </th>
                </tr>
                </thead>
                <tbody>
                {#each Object.keys(prediction) as key}
                    <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                        <th scope="row" class="px-3 py-2 font-medium text-gray-900 whitespace-nowrap dark:text-white">
                            {key}
                        </th>
                        <td class="px-3 py-2">
                            {prediction[key]}
                        </td>
                    </tr>
                {/each}
                </tbody>
            </table>
        {/if}
    </div>
</div>
