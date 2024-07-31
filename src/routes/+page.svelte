<svelte:options runes />

<script lang="ts">
	import { DataTable } from '@careswitch/svelte-data-table';
	import * as Table from '$lib/components/ui/table';

	const table = new DataTable({
		data: [
			{ id: 1, name: 'John Doe', status: 'active' },
			{ id: 2, name: 'Jane Doe', status: 'inactive' }
		],
		columns: [
			{ id: 'id', key: 'id', name: 'ID' },
			{ id: 'name', key: 'name', name: 'Name' },
			{ id: 'status', key: 'status', name: 'Status' }
		]
	});
</script>

<div class="mx-auto mt-8 max-w-3xl">
	<Table.Root>
		<Table.Header>
			<Table.Row class="sticky top-0 z-10 *:bg-background">
				{#each table.columns as column (column.id)}
					<Table.Head>
						<button
							class="flex items-center"
							onclick={() => table.toggleSort(column.id)}
							disabled={!table.isSortable(column.id)}
						>
							{column.name}
							{#if table.isSortable(column.id)}
								<span class="ml-2">
									{#if table.getSortState(column.id) === 'asc'}
										<svg
											class="h-4 w-4"
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 20 20"
											fill="currentColor"
										>
											<path fill-rule="evenodd" d="M10 3l7 9H3l7-9z" />
										</svg>
									{:else if table.getSortState(column.id) === 'desc'}
										<svg
											class="h-4 w-4"
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 20 20"
											fill="currentColor"
										>
											<path fill-rule="evenodd" d="M10 17l-7-9h14l-7 9z" />
										</svg>
									{:else}
										<svg
											class="h-4 w-4"
											xmlns="http://www.w3.org/2000/svg"
											viewBox="0 0 20 20"
											fill="currentColor"
										>
											<path fill-rule="evenodd" d="M10 3l7 9H3l7-9zm0 14l-7-9h14l-7 9z" />
										</svg>
									{/if}
								</span>
							{/if}
						</button>
					</Table.Head>
				{/each}
				<Table.Head></Table.Head>
			</Table.Row>
		</Table.Header>
		<Table.Body>
			{#each table.rows as row (row.id)}
				<Table.Row>
					<Table.Cell>
						{row.id}
					</Table.Cell>
					<Table.Cell>
						{row.name}
					</Table.Cell>
					<Table.Cell>
						{row.status}
					</Table.Cell>
				</Table.Row>
			{/each}
		</Table.Body>
	</Table.Root>
</div>
