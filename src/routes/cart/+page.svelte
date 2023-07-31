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
														{#if cartItems.length == 0}
															<h1 class="nomeals">No items added</h1>
														{/if}
														{#if cartItems.length != 0}
															<ul class="meleo">
																{#each cartItems as meal, i}
																	<div class="mels">
																		<li>
																			<img src={meal.strMealThumb} alt="" style="width: 200px;" />
																		</li>
																		<li>{meal.strMeal}</li>
																		<li>
																			<button class="btn" on:click={() => removeFromCart(i)}
																				>remove from cart</button
																			>
																		</li>
																	</div>
																{/each}
															</ul>
														{/if}
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
