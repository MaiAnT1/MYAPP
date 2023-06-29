<script>
	let name = '';

	let data=[];
	let Data;
	
	//get data
  	async function loadData(){
    	const res = await fetch('http://localhost:3000/todos');
    	data = await res.json();
		console.log(data);

  	}

	//check
    async function handleClick() {
		const data = name;
		const dt = await fetch('http://localhost:3000/todos', {
			method: "POST",
			headers: {
          		"Content-Type": "application/json",
        	},
			body: JSON.stringify({
          	description: data,
			isDone: false,
          	isImportant: false,
			
        }),
		})
		Data = await dt.json();
		loadData();
	}
  	loadData();
	// Put
	function dtchange(id, data) {
		console.log(id);
		fetch ('http://localhost:3000/todos' + '/' + id, {
			method: "PUT",
			headers: {
        		"Content-Type": "application/json",
      		},
      		body: JSON.stringify(data),
			
		})
	}
</script>

<h2>To-Do List</h2>

<input bind:value={name} placeholder="enter your name" />
<p> {name || 'stranger'}</p>


<button on:click={handleClick}> Click me </button>

<ul>
	{#each data as { id, description, isDone }, i}
		<li>
			<p>
				<input type="checkbox" bind:checked={isDone} on:change={()=> {dtchange(id, {id, description, isDone })}} />
				{i + 1}: {description}
			</p>
		</li>
	{/each}
</ul>




<style>
	h1 {
		color: #002765;
    	display: flex;
    	align-items: center;
    	margin-bottom: 20px;
	}
</style>