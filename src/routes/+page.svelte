<!-- <script>
    
	const fetchImage = (async () => {
		const response = await fetch('https://dog.ceo/api/breeds/image/random');
		return await response.json();
	})();
</script>

{#await fetchImage}
	<p>.......</p>
{:then data}
	{console.log(data)}
	<p>{data.message}</p>
{:catch error}
	<p>error</p>
{/await} -->
<script>
	// @ts-nocheck

	import { onMount } from 'svelte';
	const fetchImages = (async () => {
		const response = await fetch(' https://www.themealdb.com/api/json/v1/1/filter.php?a=American');
		return await response.json();
	})();

	// @ts-ignore
	let cartItems = [];

	onMount(() => {
		const cartItemsFromStorage = localStorage.getItem('cartItems');
		if (cartItemsFromStorage) {
			cartItems = JSON.parse(cartItemsFromStorage);
		}
	});

	// @ts-ignore
	function addToCart(product) {
		// @ts-ignore
		cartItems = [...cartItems, product];
		localStorage.setItem('cartItems', JSON.stringify(cartItems));
		window.alert('item added');
		console.log(cartItems);
	}

	// @ts-ignore
	function calculateTotalCost() {
		// @ts-ignore
		return 500 * cartItems.length;
	}
</script>

<link rel="stylesheet" href="/node_modules/@fortawesome/fontawesome-free/css/all.min.css" />
<main>
	<div class="inner-body">
		<div class="topbar">
			<input type="text" /><i class="fa-solid fa-search" />
			<h1>Menu:</h1>
		</div>
		<div class="inner-body-2">
			<div class="sidebar">
				<a href="/" style="color: black; margin-top:30px;"><i class="fa-solid fa-home" /></a>
				<p>home</p>
				<a href="/cart" style="color: black; margin-top:30px;"
					><i class="fa-solid fa-cart-shopping" /></a
				>
				<p>order</p>
				<a href="/cart" style="color: black; margin-top:30px;"><i class="fa-solid fa-user" /></a>
				<p>user</p>
			</div>
			<div class="display">
				<div class="menu">
					{#await fetchImages}
						<p>.......Loading Dishes.....</p>
					{:then data}
						<ul class="meleo">
							{#each data.meals as meal, i}
								<div class="mels">
									<li><img src={meal.strMealThumb} alt="" style="width: 200px;" /></li>
									<li>{meal.strMeal}</li>
									<li><button class="btn" on:click={() => addToCart(meal)}>add to cart</button></li>
								</div>
							{/each}
						</ul>
					{:catch error}
						<p>error</p>
					{/await}
				</div>
				<div class="order-subtotal">
					<h2>Total</h2>

					<!-- <ul>{cartItems.map((i) => i.strMeal)}</ul> -->
					<ul style="list-style: none;">
						{#each cartItems as item}
							<li>{item.strMeal}</li>
						{/each}
					</ul>
					<br />
					<h2>Cost: Rs{500 * cartItems.length}</h2>
					<h4>Tax:Rs{500 * cartItems.length * 0.18}</h4>
					<h1>Total:{500 * cartItems.length + 500 * cartItems.length * 0.18}</h1>
					<br />
					<a href="/cart" class="btn" style="text-decoration: none;">Move to Cart</a>
				</div>
			</div>
		</div>
	</div>
</main>

<style>
	/* width */
	::-webkit-scrollbar {
		width: 10px;
	}

	/* Track */
	::-webkit-scrollbar-track {
		background: #f1f1f1;
	}

	/* Handle */
	::-webkit-scrollbar-thumb {
		background: #888;
	}

	/* Handle on hover */
	::-webkit-scrollbar-thumb:hover {
		background: #555;
	}
	main {
		background: rgb(223, 223, 222);
		background: linear-gradient(
			180deg,
			rgba(223, 223, 222, 1) 35%,
			rgba(245, 231, 177, 1) 100%,
			rgb(240, 192, 145) 100%
		);
		font-family: 'Courier New', Courier, monospace;
	}
	.inner-body-2 {
		display: flex;
		background-color: rgb(251, 248, 248, 0.6);
		display: flex;
	}
	.menu {
		width: 80%;
	}
	.meleo {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 20px;
		list-style: none;
		align-items: center;
		background-color: rgb(255, 255, 255, 0.5);
		max-height: 600px;
		overflow: auto;
	}

	.meleo li {
		text-align: center;
	}
	.display {
		display: flex;
	}
	.order-subtotal {
		position: sticky;
		background-color: rgb(255, 255, 255, 0.9);
		padding: 50px;
	}
	.mels {
		background-color: rgb(255, 255, 255, 0.7);
		padding: 20px;
		border-radius: 10px;
		cursor: pointer;
	}
	.mels li {
		margin-bottom: 10px;
		cursor: pointer;
	}
	.sidebar {
		margin-top: 30px;
	}
	.btn {
		background-color: orange;
		color: white;
		cursor: pointer;
		border-radius: 10px;
		padding: 15px;
		font-size: 1.2rem;
		font-family: 'Courier New', Courier, monospace;
	}
	.btn:hover {
		background-color: rgb(184, 126, 20);
	}
	.topbar input {
		margin-top: 20px;
		margin-left: 30px;
		background-color: white;
		padding: 9px;
		border: none;
		width: 60vh;
		border-radius: 5px;
	}
	.topbar i {
		background-color: white;
		padding: 8px;
		margin-top: 5px;
		cursor: pointer;
		border-radius: 2px;
	}
</style>
