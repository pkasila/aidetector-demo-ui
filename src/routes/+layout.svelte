<script>
    import "../app.css";

    let y;
</script>

<div class="sticky top-0 z-50 px-6 py-6 lg:px-8 transition-colors border-gray-200 dark:border-gray-700"
     class:bg-white={y > 12} class:dark:bg-gray-900={y > 12} class:border-b={y > 12}>
    <div>
        <nav class="flex h-9 items-center justify-between" aria-label="Global">
            <div class="flex lg:min-w-0 lg:flex-1" aria-label="Global">
                <a href="/" class="-m-1.5 p-1.5">
                    <span class="sr-only">Распазнаванне малюнкаў</span>
                    <img class="h-12" src="/logo_lbsu.svg" alt="">
                </a>
            </div>
            <div class="flex lg:hidden">
                <!--
                    <button type="button"
                        class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700">
                    <span class="sr-only">Open main menu</span>
                    <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                         stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                        <path stroke-linecap="round" stroke-linejoin="round"
                              d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5"/>
                    </svg>
                </button>
                -->
            </div>
            <div class="hidden lg:flex lg:min-w-0 lg:flex-1 lg:justify-center lg:gap-x-12">
                <a data-sveltekit-preload-data="hover" href="/"
                   class="font-semibold text-gray-900 hover:text-gray-900 transition-colors
                    dark:text-gray-100 dark:hover:text-gray-300">Галоўная</a>

                <a data-sveltekit-preload-data="hover" href="/demo"
                   class="font-semibold text-gray-900 hover:text-gray-900 transition-colors
                    dark:text-gray-100 dark:hover:text-gray-300">Дэманстрацыя</a>

                <!-- <a href="#" class="font-semibold text-gray-900 hover:text-gray-900">Team</a>
                -->
            </div>
            <div class="hidden lg:flex lg:min-w-0 lg:flex-1 lg:justify-end">
                <!-- <a href="#"
                   class="inline-block rounded-lg px-3 py-1.5 text-sm font-semibold leading-6 text-gray-900 shadow-sm ring-1 ring-gray-900/10 hover:ring-gray-900/20">Log
                    in</a>-->
            </div>
        </nav>
        <!-- Mobile menu, show/hide based on menu open state.
        <div role="dialog" aria-modal="true">
            <div focus="true" class="fixed inset-0 z-10 overflow-y-auto bg-white px-6 py-6 lg:hidden">
                <div class="flex h-9 items-center justify-between">
                    <div class="flex">
                        <a href="#" class="-m-1.5 p-1.5">
                            <span class="sr-only">PicturesqueAI</span>
                            <img class="h-12" src="/logo.png" alt="">
                        </a>
                    </div>
                    <div class="flex">
                        <button type="button"
                                class="-m-2.5 inline-flex items-center justify-center rounded-md p-2.5 text-gray-700">
                            <span class="sr-only">Close menu</span>
                            <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                                 stroke-width="1.5" stroke="currentColor" aria-hidden="true">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12"/>
                            </svg>
                        </button>
                    </div>
                </div>
                <div class="mt-6 flow-root">
                    <div class="-my-6 divide-y divide-gray-500/10">
                        <div class="space-y-2 py-6">
                            <a href="#"
                               class="-mx-3 block rounded-lg py-2 px-3 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-400/10">Product</a>

                            <a href="#"
                               class="-mx-3 block rounded-lg py-2 px-3 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-400/10">Catalog</a>

                            <a href="#"
                               class="-mx-3 block rounded-lg py-2 px-3 text-base font-semibold leading-7 text-gray-900 hover:bg-gray-400/10">Team</a>
                        </div>
                        <div class="py-6">
                            <a href="#"
                               class="-mx-3 block rounded-lg py-2.5 px-3 text-base font-semibold leading-6 text-gray-900 hover:bg-gray-400/10">Log
                                in</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        -->
    </div>
</div>

<slot/>

<svelte:window bind:scrollY={y}/>
