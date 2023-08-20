<script>
	import Add from '~icons/material-symbols/add-rounded';
	import Cross from '~icons/charm/cross';
	let nombreNuevo, aporteNuevo;
	let personas = [
		{ nombre: 'Juan', aporte: 1000 },
		{ nombre: 'Pedro', aporte: 2000 },
		{ nombre: 'María', aporte: 3000 },
		{ nombre: 'José', aporte: 4000 }
	];
	let a;
	let aniadir = () => {
		//Check that the name is not empty, not repeatedm and the amount is a number
		if (nombreNuevo === undefined) return;
		if (personas.find((p) => p.nombre === nombreNuevo)) return;
		if (aporteNuevo == undefined) aporteNuevo = 0;
		personas = [...personas, { nombre: nombreNuevo, aporte: aporteNuevo }];
		nombreNuevo = undefined;
		aporteNuevo = undefined;
	};
	let remover = (persona) => {
		personas = personas.filter((p) => p.nombre !== persona.nombre);
	};
</script>

<div class="flex flex-col h-screen">
	<div class="flex justify-between items-center p-4">
		<p class="text-xl font-bold">Cuenta Clara</p>
	</div>
	<table class="table table-zebra table-fixed">
		<thead>
			<tr>
				<th class="w-1/3">Nombre</th>
				<th class="w-1/4">Aporte</th>
				<th class="w-1/4">Deuda</th>
				<th />
			</tr>
		</thead>
		<tbody>
			{#each personas as persona}
				<tr>
					<td
						><p class="">
							{persona.nombre}
						</p>
					</td>
					<td>{persona.aporte}</td>
					<td>
						<div class={`badge ${a < 0 ? 'badge-success' : 'badge-error'}`}>
							{(a =
								(personas.reduce((a, b) => a + b.aporte, 0) / personas.length).toFixed(0) -
								persona.aporte)}
						</div>
					</td>
					<td>
						<button
							on:click={() => {
								remover(persona);
							}}
						>
							<Cross class="w-7 h-7" />
						</button>
					</td>
				</tr>
			{/each}
			<tr>
				<td
					><input
						bind:value={nombreNuevo}
						type="text"
						placeholder="Nombre"
						class="input-sm input input-bordered w-20"
					/></td
				>
				<td
					><input
						bind:value={aporteNuevo}
						type="number"
						placeholder="Aporte"
						class="input-sm input input-bordered w-20"
					/></td
				>
				<td />
				<td
					><button on:click={aniadir}>
						<Add class="w-7 h-7" />
					</button></td
				>
			</tr>
		</tbody>
	</table>
</div>
