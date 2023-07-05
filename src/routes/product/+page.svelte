<script>
    
    let products = [];
    let categories = [];

    async function fetchProduct() {
        
        let res = await fetch('http://localhost:3000/products');
        products = await res.json();
        console.log(products)
    }
    fetchProduct();

    async function fetchCategory() {
        
        let res = await fetch('http://localhost:3000/products');
        categories = await res.json();
        console.log(categories)
    }
    fetchCategory();

</script>


<h1>Product list</h1>


</div>

<div>
    {#each products as product}
        <div>
            <img src="{product.thumbnailUrl}" alt="{product.title}">
            <span>{product.title}</span>
            <a href="{product.url}">View</a>
        </div>
    {/each}
</div>

<div>
    {#each categories as category}
        <div>
            <button on:click={() =>{}}>{category.title}</button>
        </div>
    {/each}
</div>