<script>
    
	let name = '';

	let data=[];
	let Data;
	let newdata = [];
	//get data
  	async function loadData(){
    	const res = await fetch('http://localhost:3000/todos');
    	data = await res.json();
		console.log(data);

  	}

	//post
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
		
	}
  	
	// put
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
	//delete 
	function spanClick(id, data) {
		console.log(id);
		fetch ('http://localhost:3000/todos'+'/'+ id, {
			method: "DELETE",
			headers: {
        		"Content-Type": "application/json",
      		},
      		body: JSON.stringify(data),
		})
        .catch(function(){
            console.log("Error");
        })
	}

	async function dtdata(id) {
		// const newData = {value: description} ;
		const dt = await fetch('http://localhost:3000/todos' + '/' + id, {
			method: "PUT",
			headers: {
          		"Content-Type": "application/json",
        	},
			body: JSON.stringify({
          	description: newdata,
			isDone: false,
          	isImportant: false,
			
        }),
		})
		Data = await dt.json();
		loadData();
	}
  	loadData();

	
</script>

<h2>To-Do List</h2>

<input bind:value={name} placeholder="enter your name" />
<p> {name || 'stranger'}</p>


<button on:click={handleClick}> Click me </button>


<ul>
	{#each data as { id, description, isDone }, i}
		<li>
			<p>
				<input type="checkbox" bind:checked={isDone} on:change={()=> {dtchange(id, {id, description, isDone })}} class="check" />

				<s>{#if isDone}{description}{/if}</s>{#if !isDone}{description}{/if}

				<input type="text" bind:value={description} on:change={()=> {dtdata(id, newdata= {id, description, isDone })}}>
				<button class="edit" on:click{editClick}> EDIT </button>
				

				<button class="span" on:click={()=> {spanClick(id, { })}}> X </button>
			</p>
		</li>
	{/each}
</ul>





<style>
	h2 {
		color: #002765;
    	display: flex;
    	align-items: center;
    	margin-bottom: 20px;
	}

	.span {
		position: absolute;
    	right: 270px;
		border-radius: 30px;
   		background: #ffffff;
   		color: red;	
		
	}

	.edit {
		position: absolute;
    	right: 300px;
	}
</style>