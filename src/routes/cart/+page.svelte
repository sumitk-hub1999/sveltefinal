<!-- <script context="module">
  export async function load({ fetch }) {
    const response = await fetch('https://www.themealdb.com/api/json/v1/1/search.php?s=');
    const data = await response.json();
    return { meals: data.meals };
  }
</script>

<script>
  export let meals;
</script>

<main>
  <h1>Meal List</h1>
  <ul>
    {#each meals as meal}
      <li>{meal.strMeal}</li>
    {/each}
  </ul>
</main> -->
<script>
	// @ts-nocheck

	import { onMount } from 'svelte';
	// const fetchImages = (async () => {
	// 	const response = await fetch(' https://www.themealdb.com/api/json/v1/1/filter.php?a=American');
	// 	return await response.json();
	// })();

	// @ts-ignore
	let cartItems = [];

	onMount(() => {
		const cartItemsFromStorage = localStorage.getItem('cartItems');
		if (cartItemsFromStorage) {
			cartItems = JSON.parse(cartItemsFromStorage);
		}
	});
	const removeFromCart = (index) => {
		cartItems.splice(index, 1);
		localStorage.setItem('cartItems', JSON.stringify(cartItems));
		cartItems = [...cartItems];
		window.alert('meal removed');
	};
</script>

<link rel="stylesheet" href="/node_modules/@fortawesome/fontawesome-free/css/all.min.css" />
<main>
	<div class="inner-body">
		<div class="topbar">
			<input type="text" /><i class="fa-solid fa-search" />
			<h1>Your Order:</h1>
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
					{#if cartItems.length == 0}
						<h1 class="nomeals">No items added</h1>
					{/if}
					{#if cartItems.length != 0}
						<ul class="meleo">
							{#each cartItems as meal, i}
								<div class="mels">
									<li><img src={meal.strMealThumb} alt="" style="width: 200px;" /></li>
									<li>{meal.strMeal}</li>
									<li>
										<button class="btn" on:click={() => removeFromCart(i)}>remove from cart</button>
									</li>
								</div>
							{/each}
						</ul>
					{/if}
					<div class="order-subtotal">
						<h2>Total</h2>

						<br />
						<h2>Cost: Rs{500 * cartItems.length}</h2>
						<h4>Tax:Rs{500 * cartItems.length * 0.18}</h4>
						<h1>Total:{500 * cartItems.length + 500 * cartItems.length * 0.18}</h1>
						<a href="/cart" class="btn" style="text-decoration: none;font-size:0.8rem;"
							>Proceed to Pay</a
						>
						<br />
					</div>
				</div>
				<!-- <div class="order-subtotal">
					<h2>Total</h2>

					<ul>{cartItems.map((i) => i.strMeal)}</ul>
					<ul>
						{#each cartItems as item}
							<li>{item.strMeal}</li>
						{/each}
					</ul>
					<br />
				<h2>Cost: Rs{500 * cartItems.length}</h2>
					<h4>Tax:Rs{500 * cartItems.length * 0.18}</h4>
					<h1>Total:{500 * cartItems.length + 500 * cartItems.length * 0.18}</h1>
					<br />
					<a href="/cart">Move to Cart</a>
				</div> -->
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
			rgba(242, 203, 163, 1) 100%
		);
		font-family: 'Courier New', Courier, monospace;
	}
	.inner-body-2 {
		display: flex;
		background-color: rgb(251, 248, 248, 0.6);
	}
	.menu {
		width: 100%;
		display: flex;
	}
	.nomeals {
		min-width: 1200px;
		min-height: 600px;
	}
	.meleo {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 20px;
		list-style: none;
		align-items: center;
		background-color: rgb(255, 255, 255, 0.5);
		min-width: 1200px;

		max-height: 600px;
		overflow: auto;
	}

	.meleo li {
		text-align: center;
	}
	.display {
		display: flex;
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
	.order-subtotal {
		position: sticky;
		background-color: rgb(255, 255, 255, 0.9);
		padding: 50px;
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
