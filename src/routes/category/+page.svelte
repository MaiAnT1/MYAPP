<script>
	let products= [];
    let textCategory;
    let Datas;
    let data=[];
    // let data= {
    //     categoryId,
    //     id,
    //     title,
    //     url,
    //     thumbnailUrl,
    // };
    let category=[] ;
	// get data
  	async function fetchProduct(){
    	const res = await fetch('http://localhost:3000/products');
    	products = await res.json();
		console.log(products);
    }
    fetchProduct();

    async function handleClick() {
		const Data = data;
		const dt = await fetch('http://localhost:3000/todos', {
			method: "POST",
			headers: {
          		"Content-Type": "application/json",
        	},
			body: JSON.stringify(
                categoryId = textCategory
            ),
		})
		Datas = await dt.json();
		
	}
</script>
<!-- <input type="text" bind:value={textCategory} placeholder="Product"  on:change={()=> {handleClick( {data })}}/>
<button on:click={handleClick}> Click me </button> -->

<div>
    {#each category as {categoryId}}
        <div>
            <input type="text" bind:value={textCategory} placeholder="Product"  on:change={()=> {handleClick( {categoryId})}}/>
        
            
        </div>
    {/each}
</div>