<script lang="ts">
	export let imgPath: string;
</script>

<img src={imgPath} alt={imgPath.split("/")[1].split(".")[0]} class="mb-4 mx-3 w-[45px] object-contain">