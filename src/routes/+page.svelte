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

<main>
	<div class="container-fluid d-flex flex-column">
		<div class="card bg-light text-dark d-flex flex-column">
			<div class="card-body w-100">
				<div class="d-flex flex-column w-100">
					<div class="col-md-3">
						<div class="topbar mb-4">
							<input type="text" class="form-control" placeholder="Search" style="width: 100%;" />

							<h1 class="ml-4">Menu:</h1>
						</div>
					</div>
					<div class="col-md-9 w-100">
						<div class="card bg-light">
							<div class="card-body">
								<div class="row">
									<div class="col-md-6 d-flex">
										<div class="sidebar">
											<a href="/" style="color: black; margin-top: 10px;"
												><i class="fa-solid fa-home" /></a
											>
											<p>home</p>
											<a href="/cart" style="color:black; margin-top: 10px;"
												><i class="fa-solid fa-cart-shopping" /></a
											>
											<p>order</p>
											<a href="/cart" style="color: black; margin-top: 10px;"
												><i class="fa-solid fa-user" /></a
											>
											<p>user</p>
										</div>
										<div class="col-md-1" />
										<div class="card bg-light w-100 container-fluid col-md-9">
											<div class="card-body row w-100">
												<div class="display w-100">
													<div class="menu w-100" style=" overflow-y: auto;">
														{#await fetchImages}
															<p>.......Loading Dishes.....</p>
														{:then data}
															<ul
																class="meleo d-flex flex-wrap justify-content"
																style="margin-bottom: 0;flex-grow: 1;"
															>
																{#each data.meals as meal, i}
																	<div class="mels">
																		<li>
																			<img src={meal.strMealThumb} alt="" style="width: 200px;" />
																		</li>
																		<li>
																			{meal.strMeal.length >= 20
																				? meal.strMeal.slice(0, 20) + '...'
																				: meal.strMeal}
																		</li>
																		<li>
																			<button class="btn" on:click={() => addToCart(meal)}
																				>add to cart</button
																			>
																		</li>
																	</div>
																{/each}
															</ul>
														{:catch error}
															<p>error</p>
														{/await}
													</div>
												</div>
											</div>
										</div>
									</div>
									<div class="col-md-3" />
									<div class="col-md-3">
										<div class="card bg-light">
											<div class="card-body">
												<h2>Total</h2>
												<ul>
													{#each cartItems as item}
														<li>{item.strMeal}</li>
													{/each}
												</ul>
												<br />
												<h2>Cost: Rs{500 * cartItems.length}</h2>
												<h4>Tax: Rs{500 * cartItems.length * 0.18}</h4>
												<h1>Total: {500 * cartItems.length + 500 * cartItems.length * 0.18}</h1>
												<br />
												<a href="/cart" class="btn" style="text-decoration: none;">Move to Cart</a>
											</div>
										</div>
									</div>
								</div>
							</div>
						</div>
					</div>
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

	.menu {
		width: 100%;
	}
	.meleo {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 20px;
		width: 100vh;
		list-style: none;
		align-items: center;
		background-color: rgb(255, 255, 255, 0.5);
		max-height: 500px;
		overflow-y: auto;
		overflow-x: hidden;
	}
	.meleo::-webkit-scrollbar {
		width: 10px;
	}

	.meleo::-webkit-scrollbar-track {
		background: transparent;
	}

	.meleo::-webkit-scrollbar-thumb {
		background: #888;
	}

	.meleo::-webkit-scrollbar-thumb:hover {
		background: #555;
	}
	.meleo .mels {
		width: calc(33.33% - 20px);
		margin-bottom: 20px;
		padding: 10px;
		background-color: rgba(255, 255, 255, 0.7);
		border-radius: 10px;
		cursor: pointer;
	}

	.meleo li {
		text-align: center;
	}
	.display {
		display: flex;
		width: 100vh;
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

	@media (max-width: 768px) {
		.inner-body-2 {
			flex-direction: column;
		}

		.menu {
			width: 100%;
		}

		.order-subtotal {
			position: static;
			padding-top: 20px;
			background-color: transparent;
		}

		.topbar input {
			width: 100%;
		}

		.topbar i {
			margin-left: 10px;
		}
	}

	@media (max-width: 576px) {
		.meleo {
			grid-template-columns: repeat(1, 1fr);
		}
		.meleo li {
			font-size: 10px;
		}
		.meleo li img {
			height: 100px;
			width: auto;
		}
		.meleo li button {
			font-size: 10px;
			padding: 1px;
		}
	}
</style>
