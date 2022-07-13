<script>
	import Product from "./Product.svelte";
	import Button  from "./Button.svelte";
	import Cart from "./Cart.svelte"

	let title = '';
	let price = 0;
	let description = '';

	let products = [];
	let cartItems = [];

	function createProduct() {
		const newProduct = {
			title: title,
			price: price,
			description: description
		};

		products = [...products, newProduct];
	}

	function addToCart(event) {
		const selectedTitle = event.detail;
		cartItems = [...cartItems, products.find(prod => prod.title === selectedTitle)];
		console.log(cartItems);
	}

</script>


<style>
	main {
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	section {
		width: 30rem;
		margin: auto;
	}

	input, label, textarea {
		width: 100%;
	}

	@media (min-width: 640px) {
		main {
			max-width: 30rem;
		}
	}

</style>

<svelte:head>
	<html lang="en" />
	<title>Cart App</title>
</svelte:head>

<section>
	<Cart items={cartItems}></Cart>
</section>

<hr>

<section>
	<div>
		<label for="title">Title</label>
		<input type="text" id="title" bind:value={ title }>
	</div>
	<div>
		<label for="price">Price</label>
		<input type="number" id="price" bind:value={ price }>
	</div>
	<div>
		<label for="description">description</label>
		<textarea rows="3" id="description" bind:value={ description }></textarea>
	</div>

	<Button on:click={createProduct}>Create Product</Button>

</section>

<main>
	{#if products.length === 0}
	<p>No products added yet!</p>
	{:else}
	{#each products as product}
	<Product 
	productTitle={ product.title } 
	productPrice={ product.price } 
	productDescription={ product.description }
	on:addCart={addToCart} />
	{/each}
	{/if}
</main>
