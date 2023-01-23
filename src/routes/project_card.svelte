<script lang="ts">
    export let customer: string;
    export let role: string;
    export let img: string;
</script>

<article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] rounded-md w-[340px] h-[340px] relative">
    <img class="w-full object-cover rounded-md" src={img} alt={`${role} at ${customer}`} />
    <div class="bottom-0 left-0 right-0 top-8 absolute bg-gradient-to-t from-[rgba(0,0,0,0.8)] to-[rgba(0,0,0,0)]"></div>
    <div class="absolute bottom-0 left-0 right-0 p-3">
        <h3 class="font-semibold text-xl">{customer}</h3>
        <p>{role}</p>
    </div>
</article>