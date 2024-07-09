<script lang="ts">
	import DialogEditItem from './DialogEditItem.svelte';

	let items: Array<string> = ['First', 'Second', 'Third'];
	let itemInput: string = '';

	let showDialog: boolean = false;
	let inputDialog: string = '';
	let indexItemEditable: number = -1;

	const editItemByIndex = (index: number) => {
		return () => {
			showDialog = true;
			indexItemEditable = index;
			inputDialog = items[index];
		};
	};

	const saveItemEdit = (inputDialog: string) => {
		items[indexItemEditable] = inputDialog;
		showDialog = false;
	};

	const removeItemByIndex = (index: number) => {
		return () => {
			items[index] = '';
		};
	};

	const appendItem = () => {
		items.push(itemInput);
		items = [...items];
	};

	const cleanAllTable = () => {
		items = [];
	};

	$: {
		items = items.filter((n) => n.length > 0);
	}
</script>

<table>
	<caption>Table data</caption>

	<thead>
		<tr>
			<th colspan="3">
				<input type="text" placeholder="Put your item" bind:value={itemInput} />
				<button>Search</button>
				<button on:click={appendItem}>Append</button>
			</th>
		</tr>
		<tr>
			<th>ID</th>
			<th>Item</th>
			<th>Controls</th>
		</tr>
	</thead>

	<tbody>
		{#each items as item, i}
			<tr>
				<th>{i}</th>
				<td>
					{item}
				</td>
				<th>
					<button on:click={removeItemByIndex(i)}>Remove</button>
					<button on:click={editItemByIndex(i)}>Edit</button>
				</th>
			</tr>
		{/each}
	</tbody>

	<tfoot>
		<tr>
			<th colspan="3">
				Table controls
				<button on:click={cleanAllTable}>Clean</button>
				<button>Save</button>
			</th>
		</tr>
	</tfoot>
</table>

<DialogEditItem bind:show={showDialog} bind:input={items[indexItemEditable]} />

<style>
	table,
	th,
	td {
		border: 1px solid black;
	}
</style>
