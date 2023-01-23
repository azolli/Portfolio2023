<script lang="ts">
    import { spring } from "svelte/motion";

    export let customer: string;
    export let role: string;
    export let img: string;

    let cardDescOpacity = spring(0);

    const show = () => {
        cardDescOpacity.set(1)
    };

    const hide = () => {
        cardDescOpacity.set(0)
    };

</script>

<article on:focus={show} on:mouseover={show} on:mouseleave={hide} class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] rounded-md w-[340px] h-[340px] relative">
    <img class="w-full object-cover rounded-md" src={img} alt={`${role} at ${customer}`} />
    <div class="bottom-0 left-0 right-0 top-8 absolute bg-gradient-to-t from-[rgba(0,0,0,0.8)] to-[rgba(0,0,0,0)]" style="opacity:{$cardDescOpacity}"></div>
    <div class="absolute bottom-0 left-0 right-0 p-3" style="opacity:{$cardDescOpacity}; transform: translateY(-{$cardDescOpacity*3}px)">
        <h3 class="font-semibold text-xl">{customer}</h3>
        <p>{role}</p>
    </div>
</article>