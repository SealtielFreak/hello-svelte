<script lang="ts">
	export let input: string = '';
	export let show: boolean;

	let inputValue: string = input.slice(0, input.length);

	const saveButton = () => {
		show = false;
		input = inputValue;
	};
</script>

{#if show}
	<dialog open>
		<input type="text" bind:value={inputValue} />
		<button on:click={saveButton}>Save and close</button>
	</dialog>
{/if}
