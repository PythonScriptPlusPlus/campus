<template>
	<div class="home">
		<div class="books">
			<div class="list">
				<div
					v-for="book in books"
					:key="book.id"
					class="books__wrapper"
				>
					<div
						v-if="book.amount"
						class="book"
					>
						<p class="book__name">
							{{ book.name }}
						</p>
						<p class="book__price">
							Цена: {{ book.price }}₽
						</p>
						<div
							class="book__purchase"
							@click="buy(book)"
						>
							Купить
						</div>
					</div>
				</div>
			</div>
			<div class="personal">
				Личный кабинет
				<div class="personal__bottom">
					<p class="personal__balance">
						Баланс: {{ balance }}₽
					</p>
					<p
						v-if="booksBought"
						class="personal__bought"
					>
						Вы купили {{ booksBought }} книги на сумму {{ booksPrice }}₽
					</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Home',
	data() {
		return {
			books : [
				{
					id: 1,
					name: 'Совершенный код. Мастер-класс',
					price: 100,
					amount: 3
				},
				{
					id: 2,
					name: 'Rapid Development, Steve McConnell',
					price: 180,
					amount: 2
				},
				{
					id: 3,
					name: 'Искусство программирования, Д.Кнут',
					price: 210,
					amount: 1
				},
			],
			balance : 500,
			booksBought : 0,
			booksPrice : 0,
			buy(item) {
				if (item.price <= this.balance) {
					this.balance -= item.price;
					this.booksBought++;
					this.booksPrice += item.price;
					item.amount--;
				} else {
					swal('Недостаточно средств для покупки');
				}
			}
		};
	}
};
</script>

<style lang="scss" scoped>
.list {
	overflow: auto;
	height: calc(100% - 130px);
}

.personal {
	font-weight: 900;
	font-size: 2em;
	position: absolute;
	bottom: 0;
	left: 20px;
	height: 125px;
	width: calc(100% - 40px);
	border-top: grey 1px solid;

	&__bottom {
		//display: flex;
		font-weight: 500;
		font-size: 1em;
		margin-left: 30px;
	}

	&__balance {
		margin: 0;
	}

	&__bought {
		margin: 0;
	}

}

.home {
	background-image: url('/img/background.png');
	background-size: cover;
	background-position-x: center;
	background-position-y: center;
	height: 100vh;
	position: relative;
}

.books {
	position: absolute;
	width: 70%;
	max-width: 1100px;
	aspect-ratio: 10/8;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	background: white;
	border-radius: 40px;

	&__wrapper {
		height: fit-content;
		width: 100%;
	}
}

.book {
	margin: 20px;
	display: grid;
	grid-template-columns: 1fr 1fr;
	grid-template-rows: 1fr 1fr;
	border-bottom: grey 1px solid;
	padding-bottom: 10px;
	position: relative;
	
	&__name {
		margin: 0;
		font-size: 2em;
		font-weight: 900;
		grid-column: 1/3 ;
		grid-row: 1;
	}

	&__price {
		margin: 0;
		font-style: italic;
		color: grey;
	}

	&__purchase {
		grid-row: 2/3;
		grid-column: 2/3;
		transition: border 0.2s, background .2s;
		background:rgb(80, 80, 253);
		border: 3px solid rgb(80, 80, 253);
		width: fit-content;
		height: fit-content;
		padding: 10px;
		color: white;
		border-radius: 8px;
		margin-left: 50%;
		cursor: pointer;

		&:hover {
			background:rgb(125, 125, 255);
			border: 3px solid rgb(125, 125, 255);
			transition: border 0.2s, background .2s;
		}

		&:active {
			transition: border 0.2s, background .2s;
			background: white;
		}
	}
}
</style>