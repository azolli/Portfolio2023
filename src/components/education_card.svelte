<script lang="ts">
	export let school: string;
	export let degreeType: string;
	export let year: string;
</script>

<article class="m-2 bg-black border-2 border-[rgba(50,50,50,0.5)] p-4 rounded-md w-[420px]">
	<div>
		<div class="flex items-center">
			{#if year == '0'}
				<div class="rounded-full bg-yellow-500 w-4 h-4" />
				<h5 class="ml-2 uppercase font-bold text-yellow-500">In Progress</h5>
			{:else}
				<div class="rounded-full bg-green-400 w-4 h-4" />
				<h5 class="ml-2 uppercase font-bold text-green-400">Issued in {year}</h5>
			{/if}
		</div>
		<h3 class="font-semibold text-xl">{school}</h3>
		<p>{degreeType}</p>
	</div>
</article>
