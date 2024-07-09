<script lang="ts">
	export let input: string = '';
	export let show: boolean;

	const saveButton = () => {
		show = false;
	};
</script>

{#if show}
	<dialog open>
		<input type="text" bind:value={input} />
		<button on:click={saveButton}>Save and close</button>
	</dialog>
{/if}
