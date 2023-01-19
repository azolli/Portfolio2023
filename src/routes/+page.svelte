<script>
    import { spring } from 'svelte/motion'; 

    let sectionsOpacity = spring([0,0,0,0,0]);
    let copyBannerOpacity = spring(0);
    let skillsInteractive = spring([0,0,0])

    // @ts-ignore
    let intersectionObserver;

    const ioConfiguration = {
        /**
         * This rootMargin creates a horizontal line vertically centered
         * that will help trigger an intersection at that the very point.
         */
        rootMargin: '-50% 0% -50% 0%',

        /**
         * This is the default so you could remove it.
         * I just wanted to leave it here to make it more explicit
         * as this threshold is the only one that works with the above
         * rootMargin
         */
        threshold: 0
    };

    function ensureIntersectionObserver() {
        // @ts-ignore
        if (intersectionObserver) return;

    intersectionObserver = new IntersectionObserver(
            (entries) => {
                entries.forEach(entry => {
                    const eventName = entry.isIntersecting ? 'enterViewport' : 'exitViewport';
                    entry.target.dispatchEvent(new CustomEvent(eventName));
                });
            }, ioConfiguration
        );
    }

    //@ts-ignore
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

    function elementCopied(){
        copyBannerOpacity.set(1)
        setTimeout(() => {
            copyBannerOpacity.set(0)
        },2000)   
    }

</script>

<head>
    <title>Alessandro Zolli | Portfolio</title>
    <!-- Add other meta tags -->
</head>

<div class="border-2 border-[rgba(50,50,50,0.5)] p-4 bg-black fixed bottom-5 left-5 rounded-md" style="opacity: {$copyBannerOpacity}">
    <p>Send copied text to interesting people!</p>
</div>

<nav class="fixed top-0 left-0 right-0 p-2">
    <img src="/az-logo.svg" width="50px" alt="logo" />
</nav>
<section on:copy={elementCopied}>
    <section class="flex flex-col justify-center items-center my-12 h-[80vh]" style="opacity: {$sectionsOpacity[0]}" >
        <img class="max-w-xs rounded-full my-10 border-neutral-50 border-8" use:viewport on:enterViewport={() => sectionsOpacity.set([1,0,0,0,0])} src="https://media.licdn.com/dms/image/C4E03AQH0ZQ0Xe-J4AQ/profile-displayphoto-shrink_800_800/0/1653594699142?e=1679529600&v=beta&t=VWCg-Fgt9J9gvLP2TE6nXh-5LeYDMZh8R1ixHhCW56s" alt="Alessandro Zolli" />
        <h1 class="text-4xl md:text-6xl font-semibold text-center">Hi, I'm Alessandro Zolli!</h1>
        <div class="flex my-4">
            <a target="_blank" rel="noreferrer" href="https://www.linkedin.com/in/alessandrozolli/" class="mr-2"><img src="/linkedin.png" width="30" alt="LinkedIn" /></a>
            <a target="_blank" rel="noreferrer" href="https://github.com/azolli" class="ml-2"><img src="/github.svg" width="30" alt="Github" /></a>
        </div>
    </section>
    <section class="max-w-xl mx-auto">
        <article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[1]}">
            <h1 class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600" use:viewport on:enterViewport={() => sectionsOpacity.set([0.3,1,0.3,0,0.3])}>I'm Alessandro Zolli, a 19 years old engineering student and software developer.</h1>
        </article>
        <article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[2]}">
            <h1 class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600" use:viewport on:enterViewport={() => sectionsOpacity.set([0.3,0.3,1,0.3,0.3])}>I'm based in Turin but I really like to explore new places and work remotely.</h1>
        </article>
        <article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[3]}">
            <h1 class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600" use:viewport on:enterViewport={() => sectionsOpacity.set([0.3,0.3,0.3,1,0.3])}>I started programming at 10 years old and today I work with advanced languages such as Rust and a lot of frameworks.</h1>
        </article>
        <article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[4]}">
            <h1 class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600" use:viewport on:enterViewport={() => sectionsOpacity.set([0.3,0.3,0.3,0.3,1])}>In the free time I like skiing and playing guitar.</h1>
        </article>
    </section>
    <section>
        <h2 class="text-4xl font-bold text-center my-8">Education</h2>
        <div class="flex justify-center flex-wrap">
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
                <div>
                    <div class="flex items-center">
                        <div class="rounded-full bg-yellow-500 w-4 h-4"></div>
                        <h5 class="ml-2 uppercase font-bold text-yellow-500">In Progress</h5>
                    </div>
                    <h3 class="font-semibold text-xl">Politecnico di Torino</h3>
                    <p>Engineering Bachelor Degree</p>
                </div>
            </article>
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
                <div>
                    <div class="flex items-center">
                        <div class="rounded-full bg-green-400 w-4 h-4"></div>
                        <h5 class="ml-2 uppercase font-bold text-green-400">Issued in 2022</h5>
                    </div>
                    <h3 class="font-semibold text-xl">Liceo Salesiano Valsalice</h3>
                    <p>Maturità Scientifica Opz. Sc. App. (92/100)</p>
                </div>
            </article>
        </div>
    </section>
    <section class="mt-24">
        <h2 class="text-4xl font-bold text-center my-8">IT Skills</h2>
        <div class="flex justify-center flex-wrap">
            <!-- svelte-ignore a11y-mouse-events-have-key-events -->
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
                <div>
                    <div class="flex items-center">
                        <img src="/c.png" alt="C lang" class="mb-3 mr-2 w-[40px]">
                        <img src="/rust.png" alt="Rust lang" class="mb-3 mr-2 w-[45px] h-[45px]">
                    </div>
                    <h3 class="font-semibold text-xl">Software Development</h3>
                    <p>Working as software developer to develop CLI tools, GUI applications with Qt and C/C++ and automated processes.</p>
                </div>
            </article>
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
                <div>
                    <div class="flex items-center">
                        <img src="/node.png" alt="NodeJS" class="mb-3 mr-2 w-[40px]">
                        <img src="/django.png" alt="Django" class="mb-3 mr-2 w-[45px]">
                        <img src="/react.png" alt="React" class="mb-3 mr-2 w-[40px]">
                    </div>
                    <h3 class="font-semibold text-xl">Full-stack development</h3>
                    <p>Creation of Web Applications with NodeJS or Django as backend, React (NextJS) as frontend and MongoDB or MySQL as DB.</p>
                </div>
            </article>
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
                <div>
                    <div class="flex items-center">
                        <img src="/python.png" alt="Python" class="mb-3 mr-2 w-[40px]">
                        <img src="/tensorflow.png" alt="Tensorflow" class="mb-3 mr-2 w-[40px]">
                        <img src="/opencv.webp" alt="OpenCV" class="mb-3 mr-2 w-[40px]">
                    </div>
                    <h3 class="font-semibold text-xl">Machine Learning</h3>
                    <p>I'm studying Machine Learning, specifically applied to Computer Vision on Embedded Devices.</p>
                </div>
            </article>
        </div>
    </section>
    <!-- <section class="mt-24">
        <h2 class="text-4xl font-bold text-center my-8">Portfolio</h2>
        <div class="flex justify-center flex-wrap">
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] rounded-md w-[340px] h-[340px] relative">
                <img class="w-full object-cover rounded-md" src="https://picsum.photos/1920" alt="Random" />
                <div class="bottom-0 left-0 right-0 top-8 absolute bg-gradient-to-t from-[rgba(0,0,0,0.8)] to-[rgba(0,0,0,0)]"></div>
                <div class="absolute bottom-0 left-0 right-0 p-3">
                    <h3 class="font-semibold text-xl">Digisky S.r.l.</h3>
                    <p>Embedded software developer</p>
                </div>
            </article>
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] rounded-md w-[340px] h-[340px] relative">
                <img class="w-full object-cover rounded-md" src="https://picsum.photos/1920" alt="Random" />
                <div class="bottom-0 left-0 right-0 top-8 absolute bg-gradient-to-t from-[rgba(0,0,0,0.8)] to-[rgba(0,0,0,0)]"></div>
                <div class="absolute bottom-0 left-0 right-0 p-3">
                    <h3 class="font-semibold text-xl">Digisky S.r.l.</h3>
                    <p>Embedded software developer</p>
                </div>
            </article>
            <article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] rounded-md w-[340px] h-[340px] relative">
                <img class="w-full object-cover rounded-md" src="https://picsum.photos/1920" alt="Random" />
                <div class="bottom-0 left-0 right-0 top-8 absolute bg-gradient-to-t from-[rgba(0,0,0,0.8)] to-[rgba(0,0,0,0)]"></div>
                <div class="absolute bottom-0 left-0 right-0 p-3">
                    <h3 class="font-semibold text-xl">Digisky S.r.l.</h3>
                    <p>Embedded software developer</p>
                </div>
            </article>
        </div>
    </section> -->
</section>