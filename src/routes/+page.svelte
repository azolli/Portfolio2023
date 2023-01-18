<script>
    import { spring } from 'svelte/motion'; 

    let sectionOne = spring(0);


    // @ts-ignore
    let intersectionObserver;

    function ensureIntersectionObserver() {
        // @ts-ignore
        if (intersectionObserver) return;

    intersectionObserver = new IntersectionObserver(
            (entries) => {
                entries.forEach(entry => {
                    const eventName = entry.isIntersecting ? 'enterViewport' : 'exitViewport';
                    entry.target.dispatchEvent(new CustomEvent(eventName));
                });
            }
        );
    }

    function viewport(element) {
        ensureIntersectionObserver();

        // @ts-ignore
        intersectionObserver.observe(element);

        return {
            destroy() {
                // @ts-ignore
                intersectionObserver.unobserve(element);
            }
        }
    }

</script>

<section>
    <section class="flex flex-col justify-center items-center my-12 h-[80vh]">
        <img class="max-w-xs rounded-full my-10 border-neutral-50 border-8" src="https://media.licdn.com/dms/image/C4E03AQH0ZQ0Xe-J4AQ/profile-displayphoto-shrink_800_800/0/1653594699142?e=1679529600&v=beta&t=VWCg-Fgt9J9gvLP2TE6nXh-5LeYDMZh8R1ixHhCW56s" alt="Alessandro Zolli" />
        <h1 class="text-6xl font-semibold text-center">Hi, I'm Alessandro Zolli!</h1>
    </section>
    <section>
        <article class="h-[60vh] flex flex-col justify-center">
            <h1 class="text-3xl font-semibold text-center text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">I'm Alessandro Zolli, a 19 years old engineering student and software developer.</h1>
        </article>
        <article class="h-[60vh] flex flex-col justify-center">
            <h1 class="text-3xl font-semibold text-center text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">I'm based in Turin but I really like to explore new places and work remotely.</h1>
        </article>
        <article class="h-[60vh] flex flex-col justify-center">
            <h1 class="text-3xl font-semibold text-center text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">I started programming at 10 years old and today I work with advanced languages such as Rust and a lot of frameworks.</h1>
        </article>
        <article class="h-[60vh] flex flex-col justify-center">
            <h1 class="text-3xl font-semibold text-center text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600">In the free time I like skiing and playing guitar.</h1>
        </article>
    </section>
    <section class="flex justify-center flex-wrap">
        <article class="m-2 bg-[rgb(44,42,46)] p-4 rounded-md w-[420px]">
            <div>
                <div class="flex items-center">
                    <div class="rounded-full bg-yellow-500 w-4 h-4"></div>
                    <h5 class="ml-2 uppercase font-bold text-yellow-500">In Progress</h5>
                </div>
                <h3 class="font-semibold text-xl">Politecnico di Torino</h3>
                <p>Engineering Bachelor Degree</p>
            </div>
        </article>
        <article class="m-2 bg-[rgb(44,42,46)] p-4 rounded-md w-[420px]">
            <div>
                <div class="flex items-center">
                    <div class="rounded-full bg-green-400 w-4 h-4"></div>
                    <h5 class="ml-2 uppercase font-bold text-green-400">Issued in 2022</h5>
                </div>
                <h3 class="font-semibold text-xl">Liceo Salesiano Valsalice</h3>
                <p>Maturità Scientifica Opz. Sc. App. (92/100)</p>
            </div>
        </article>
    </section>
    <section class="h-[100vh]">

    </section>
</section>