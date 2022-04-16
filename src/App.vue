<template>
	<div class="container main-row">
		<transition name="move-from-left">
			<div class="navigation__wrapper navigation"
				 v-if="showMenu"
			>
				<header>
					<div><img src="@/img/header/logo.png"></div>
					<button @click="showMenu = !showMenu"
							class="header__button-close">
						<img src="@/img/popup/cancel.png" alt="">
					</button>
				</header>
				<nav class="navigation__nav navigation-nav"
				>
					<div v-for="item in navItem"
						 :key="item.id"
						 class="navigation-nav__item navigation-nav-item"
						 :class="{'active-link' : item.active}"
					>
						<div class="navigation-nav-item__img">
							<img :src="getImg(item.src)">
						</div>
						<a :href="item.href"
						   class="navigation-nav-item__link nav-link"
						>{{item.name}}</a>
					</div>
				</nav>
			</div>
		</transition>
		<section class="management-screen">
			<div class="management-screen__header management-screen-header">
				<div class="hamburger"
				>
					<div class="hamburger-lines"
						 @click="showMenu = !showMenu"

					>
						<span class="line line1"></span>
						<span class="line line2"></span>
						<span class="line line3"></span>
					</div>
				</div>
				<div class="management-screen-header__breadcrumbs">
					<a href="#"
					   class="nav-link">
						Главная</a>
					>
					<a href="#"
					   class="nav-link">
						Мои магазины
					</a>
				</div>
				<div class="management-screen-header__message">
					<button class="message-button">
						<img src="@/img/management-screen/message.png">
						<img src="@/img/management-screen/new-message.png" class="new-message">
					</button>
				</div>
				<button class="management-screen-header__account">
					<span class="account__picture">
						<img src="@/img/management-screen/account-picture.png" alt="">
					</span>
					<span v-if="!isMobile"
						  class="account__name">Максим Должанский</span>
				</button>
			</div>
			<div class="management-screen__button">
				<div>
					<button @click="showPopup = true"
							class="button_add-store btn btn-green">
						<img src="@/img/management-screen/plus.png" alt="">
						Создать свой магазин
					</button>
				</div>
			</div>
			<div class="management-screen__title">
				<div>
					<p class="title">Управление магазинами</p>
				</div>
			</div>
			<div class="management-screen__control-block control-block">
				<div class="table">
					<div class="table__header table__row">
						<div class="table__col">
							№
						</div>
						<div class="table__col">
							Название
						</div>
						<div class="table__col">
							Адрес
						</div>
						<div class="table__col">
							Действие
						</div>
					</div>
					<div v-for="item in listStore"
						 class="table__row">
						<div class="table__col">
							{{item.number}}
						</div>
						<div class="table__col">
							{{item.name}}
						</div>
						<div class="table__col">
							{{item.href}}
						</div>
						<div class="table__col table__button">
							<button class="table__button_action btn btn-green">
								<img src="@/img/management-screen/pencil.png" alt="">
								Редактировать
							</button>
							<button class="table__button_action btn btn-gray">
								<img src="@/img/management-screen/cancel.png" alt="">
								Редактировать
							</button>
						</div>
					</div>
				</div>
			</div>
			<transition name="fade">
				<div class="management-screen__popup popup"
					 v-if="showPopup"
				>
					<div>
						<div class="popup__header">
							<p class="popup__header_title title">Создать магазин</p>
							<button @click="showPopup = false"
									class="popup__header_button-close">
								<img src="@/img/popup/cancel.png" alt="">
							</button>
						</div>
						<form class="popup__setting">
							<div class="popup__setting_select">
								<label>
									<span class="select__header">Шаблон</span>
									<select class="select__item" type="text">
										<option value="Стандартный">Стандартный</option>
										<option value="Стандартный">Стандартный 2</option>
									</select>
								</label>
								<label>
									<span class="select__header">Цветовая схема</span>
									<select class="select__item" type="text">
										<option value="Стандартный">Классическая</option>
										<option value="Стандартный">Классическая 2</option>
									</select>
								</label>
							</div>
							<div class="popup__setting_input input-domain">
								<label for="domainField">Домен</label>
								<div class="input-domain__field">
									<input id="domainField" type="text" placeholder="Например: ivangrozniy">
									<span>.work5.ru</span>
								</div>
							</div>
							<div class="popup__setting_attention">
								<div>
									<img src="@/img/popup/warning.png" alt="">
								</div>
								<p>В названии домена разрешены латиница и “-”, запрещается использовать словосочетание
									Work
									5.
									После создания магазина Вы сможете прикрутить свой домен (например ivangrozniy.ru).
									Подробнее по <a href="#">ссылке</a></p>
							</div>
							<div class="popup__setting_buttons">
								<button class="btn btn-gray">Отмена</button>
								<button class="btn btn-green">Создать</button>
							</div>
						</form>
					</div>
				</div>
			</transition>
		</section>
	</div>
</template>
<script>
    export default {
        name: 'App',
        data() {
            return {
                navItem: [
                    {
                        id: 1,
                        name: 'Главная',
                        href: '#',
                        src: 'web-page-home.png',
                        active: false,
                    },
                    {
                        id: 2,
                        name: 'Мои магазины',
                        href: '#',
                        src: 'shopping_cart.png',
                        active: true,
                    },
                    {
                        id: 3,
                        name: 'Промоматериалы',
                        href: '#',
                        src: 'megaphone.png',
                        active: false,
                    },
                    {
                        id: 4,
                        name: 'Статистика',
                        href: '#',
                        src: 'pie_chart.png',
                        active: false,
                    },
                    {
                        id: 5,
                        name: 'Баланс',
                        href: '#',
                        src: 'wallet.png',
                        active: false,
                    },
                    {
                        id: 6,
                        name: 'Персональные данные',
                        href: '#',
                        src: 'profile.png',
                        active: false,
                    },
                    {
                        id: 7,
                        name: 'FAQ',
                        href: '#',
                        src: 'information.png',
                        active: false,
                    },
                    {
                        id: 8,
                        name: 'Техподдержка',
                        href: '#',
                        src: 'music_and_multimedia.png',
                        active: false,
                    },
                    {
                        id: 9,
                        name: 'Выход',
                        href: '#',
                        src: 'logout.png',
                        active: false,
                    },
                ],
                listStore: [
                    {
                        id: 1,
                        number: '51231',
                        name: 'Дипломная работа',
                        href: 'http://www.work5.ru/services',
                    },
                    {
                        id: 2,
                        number: '123123',
                        name: 'Дипломная работа',
                        href: 'http://www.work5.ru/services',
                    },
                ],
                showMenu: true,
                showPopup: false,
                isMobile: false,
            }
        },
        methods: {
            getImg(src) {
                let a = './img/header/nav-icon/' + src
                return require('' + a)
            },
        },
        components: {},
        mounted() {
            const smallDesktopWithMediaQuery = window.matchMedia('(max-width: 1200px)')
            const tableWithMediaQuery = window.matchMedia('(max-width: 992px)')

            smallDesktopWithMediaQuery.addEventListener('change', (event) => {
                if (event.matches) {
                    this.isMobile = false;
                    this.showMenu = false
                } else {
                    this.showMenu = true
                }
            })
            tableWithMediaQuery.addEventListener('change', (event) => {
                if (event.matches) {
                    this.isMobile = true;
                } else {
                    this.isMobile = false;
                }
            })

            console.log(smallDesktopWithMediaQuery.matches)

            if (smallDesktopWithMediaQuery.matches) {
                this.showMenu = false
            }
            if (tableWithMediaQuery.matches) {
                this.isMobile = true
            }

        },
        watch: {}
    }
</script>
<style lang="scss">

	@import "~bootstrap/dist/css/bootstrap-grid.min.css";
	@import "~bootstrap/scss/bootstrap-grid";
	@import "~bootstrap/dist/css/bootstrap-reboot.min.css";
	@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500&display=swap');

	/*Variables SCSS*/
	$white: white;
	$green: #55c97b;
	$gray: #b1b1b1;
	$gray-text: #7d7d7d;
	$black-text: #343434;


	$standardFontSize: 14px;

	$user-border-radius: 5px;

	/*Bootstrap*/
	.my-row {
		@include make-row();
		margin-right: 0;
		margin-left: 0;

		& > * {
			@include make-col-ready();
		}
	}

	.container {
		max-width: 100%;
		padding: 0;
	}

	.btn {
		color: $white;
		padding: 10px 15px;
		transition: background-color .3s;
		border-radius: $user-border-radius;
	}

	.btn-green {
		background-color: $green;

		&:hover {
			background-color: #3a9758;
		}
	}

	.btn-gray {
		background-color: $gray;

		&:hover {
			background-color: #8a8a8a;
		}
	}

	/*reboot*/
	button, select, input {
		border: none;
		outline: none;
	}

	h1, h2, h3 {
		margin: 0;
	}

	a {
		text-decoration: none;
	}

	p {
		margin: 0;
	}


	/*Общие стили*/
	* {
		box-sizing: border-box;
	}


	body {
		background-color: #f8faff;
		margin: 0;
	}

	#app {
		font-family: 'Roboto', sans-serif, Avenir, Helvetica, Arial, sans-serif;
		font-weight: 500;

		font-size: $standardFontSize;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: $gray-text;
	}

	.title {
		font-size: 20px;

		color: $black-text;
	}

	.main-row {
		@extend .my-row;
		align-items: flex-start;
	}

	.nav-link {
		transition: color .3s;
		color: $gray-text;

		&:hover {
			color: $black-text;
		}
	}

	.active-link {
		margin-left: -5px;
	}

	.active-link::before {
		content: "";
		display: block;

		position: relative;
		top: 0;
		left: -20px;

		height: 55px;
		width: 5px;

		border-left: 5px solid #6666cc;

	}

	.nav-container .hamburger-lines {
		display: block;
		height: 26px;
		width: 32px;
		position: absolute;
		top: 17px;
		left: 20px;
		z-index: 2;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.hamburger {
		@include make-col();
		@include padding(0);
		display: block;
		height: 24px;
		width: 24px;
		cursor: pointer;

		@include media-breakpoint-up(xl) {
			display: none;
		}

		.hamburger-lines {
			width: 32px;
			height: 100%;
			position: relative;
		}

		.hamburger-lines .line {
			display: block;
			position: absolute;
			height: 2px;
			width: 100%;
			border-radius: 10px;
			background: $gray-text;
		}

		.hamburger-lines .line1 {
			top: 0;
			transform-origin: 0% 0%;
			transition: transform 0.4s ease-in-out;
		}

		.hamburger-lines .line2 {
			top: 50%;
			transform: translateY(-50%);
			transition: transform 0.2s ease-in-out;
		}

		.hamburger-lines .line3 {
			bottom: 0;
			transform-origin: 0% 100%;
			transition: transform 0.4s ease-in-out;
		}
	}

	/*Анимации для transition*/

	.fade-enter-active,
	.fade-leave-active {
		transition: opacity 0.5s ease;
	}

	.fade-enter-from,
	.fade-leave-to {
		opacity: 0;
	}

	.move-from-left-enter-active,
	.move-from-left-leave-active {
		transition: transform 0.5s ease;
	}

	.move-from-left-enter-from,
	.move-from-left-leave-to {
		transform: translateX(-500px);
	}

	/*Основые стили*/

	.navigation {
		background-color: $white;
		width: 255px;
		height: 100vh;
		@extend .my-row;

		flex-direction: column;
		flex-wrap: nowrap;

		overflow-y: auto;

		header {
			margin: 25px 0 15px;
			text-align: left;
			display: flex;
			justify-content: space-between;

			.header__button-close {
				@include media-breakpoint-up(xl) {
					display: none;
				}
				background-color: white;
			}
		}

		&-nav {
			@extend .my-row;
			text-align: left;
			padding: 0;

			&-item {
				@include make-col(12);
				@extend .my-row;
				align-items: center;
				line-height: 25px;

				&__img {
					$width_img: 25px;
					width: 25px;
					height: 25px;
					position: relative;

					img {
						position: absolute;
						top: 0;
						left: 0;

						transition: filter .3s;

					}
				}

				&__link {
					@include make-col();
					padding: 15px 10px;
				}

				&:hover {
					img {
						filter: brightness(0);
					}
				}
			}
		}

		@include media-breakpoint-down(xl) {
			position: fixed;
			top: 0;
			left: 0;
			z-index: 10;
		}
	}

	.management-screen {
		@extend .my-row;
		@include make-col();
		padding: 20px 35px 20px 35px;
		position: relative;

		@include media-breakpoint-down(md) {
			padding: 20px 15px 20px 15px;
		}
		@include media-breakpoint-up(md) {
			& > div:not(div.popup) {
				@include padding-left(0);
				@include padding-right(0);
			}
		}
		@include media-breakpoint-down(sm) {
			padding: 20px 5px 20px 5px;
		}


		&__header {
			@include make-col();
			@extend .my-row;

			align-items: center;

			margin-bottom: 10px;

			.management-screen-header {

				&__breadcrumbs {
					align-self: flex-start;

					@include make-col();
					text-align: left;
					font-size: 12px;

					& > .nav-link {
						color: $black-text;
					}

					@include media-breakpoint-down(xl) {
						display: none;
					}
				}

				&__message {
					@include make-col();
					position: relative;

					text-align: right;

					.message-button {
						position: relative;
						$size: 65px;
						width: $size;
						height: $size;
						border: 1px solid #d4d4d4;
						border-radius: $user-border-radius;
						background-color: transparent;

						&:hover {
							img {
								opacity: .7;
							}
						}

						& > img {
							transition: opacity .3s;
							position: relative;
						}

						.new-message {
							position: absolute;
							top: 20%;
							right: 20%;
						}
					}
				}

				&__account {
					@include make-col();

					display: flex;

					justify-content: space-evenly;

					align-items: center;


					justify-self: flex-end;
					align-self: stretch;

					max-width: 300px;

					border-radius: $user-border-radius;
					background-color: $white;
					transition: box-shadow .3s;

					&:hover {
						box-shadow: 0 0 8px 5px #eef3fe;
					}

					.account__picture {

						& > img {
							border: 5px solid #d4d4d4;
							border-radius: 50%;
							background-color: #efeeef;
						}
					}

					@include media-breakpoint-down(lg) {
						flex: 1 1 0 !important;
						@include make-col(1);
						max-width: 75px;
					}
				}
			}

			@include media-breakpoint-down(sm) {
				margin-bottom: 45px;
			}
		}

		&__button {
			text-align: left;

			margin-bottom: 35px;

			.button_add-store {

			}
		}

		&__title {
			margin-bottom: 30px;

			text-align: left;

			color: $black-text;

		}

		&__control-block {
			@extend .my-row;

			.table {
				@extend .my-row;
				@include padding(0);
				padding: 5px 30px;
				background-color: $white;

				border-radius: $user-border-radius;
				box-shadow: 0 0 8px 10px rgba(0, 0, 0, .02);

				&__header {
					@include make-col(12);
					color: $black-text;

					@include media-breakpoint-down(lg) {
						align-content: flex-start;
					}
				}

				&__row {
					@extend .my-row;
					@include make-col(12);
					align-items: center;

					&:not(:first-child) {
						border-bottom: 1px solid #e4e4e4;

						@include media-breakpoint-down(lg) {
							border-bottom: none;
						}
					}

					&:last-child {
						border: none;
					}

					@include media-breakpoint-down(lg) {
						&:first-child {
							@include make-col(2);
							flex: 0 0 120px !important;
						}

						& {
							@include make-col();
						}
					}
				}

				&__col {
					padding: 20px 5px;
					word-wrap: break-word;
					text-align: left;
				}

				&__col:first-child {
					@include make-col(1.5);
				}

				&__col:nth-child(2) {
					@include make-col();
				}

				&__col:nth-child(3) {
					@include make-col();
				}

				&__col:last-child {
					@include make-col();
					flex: 0 0 310px;
				}

				.table__button {
					display: flex;
					justify-content: space-between;

					@include media-breakpoint-down(lg) {
						padding-bottom: 0;
						flex-wrap: wrap;
					}
				}

				.table__button_action {
					@include media-breakpoint-down(lg) {
						width: 100%;
						margin-bottom: 15px;
					}
				}

				@include media-breakpoint-down(lg) {
					overflow-x: scroll;
					flex-wrap: nowrap;
					padding: 5px 10px;

					&__col:first-child {
						@include make-col(12);
					}

					&__col:nth-child(2) {
						@include make-col(12);
					}

					&__col:nth-child(3) {
						@include make-col(12);
					}

					&__col:last-child {
						@include make-col(12);
						flex: 0 0 310px;
					}
				}
			}
		}

		&__popup {
			@extend .my-row;
			@include padding(0);
			align-items: center;

			position: absolute;
			z-index: 5;
			top: 35%;
			left: 35px;

			overflow-y: scroll;

			max-width: 625px;
			width: 100%;
			padding: 20px;

			background-color: $white;
			box-shadow: 0 0 8px 5px rgba(0, 0, 0, .02);

			text-align: left;

			.popup {
				@extend .my-row;

				&__header {
					display: flex;
					justify-content: space-between;
					align-items: flex-start;
					margin-bottom: 50px;

					&_title {
					}

					&_button-close {
						transition: opacity .3s;
						background-color: transparent;

						&:hover {
							opacity: .7;
						}
					}
				}

				&__setting {
					@extend .my-row;

					select, input {
						padding: 12px 0;
					}

					&_select {
						display: flex;
						justify-content: space-between;
						margin-bottom: 30px;

						& > * {
							@include make-col(5);
							border-radius: $user-border-radius;
							border: 1px solid #cdcdcd;
						}

						& select {
							width: 90%;
							height: 100%;
							margin: 0 5%;
							color: $gray-text;
							background-color: transparent;
						}

						& select option {
							color: $black-text;
							background-color: transparent;
						}

						label {
							position: relative;
						}

						.select__header {
							position: absolute;
							top: -30px;
							left: 0;

							color: $black-text;
						}
					}

					&_input {
						display: flex;
						flex-direction: column;
						margin-bottom: 30px;

						label {
							margin-bottom: 5px;
						}

						input {
							display: block;
							padding-left: 15px;
						}
					}

					&_attention {
						@extend .my-row;
						@include padding(0);
						align-items: center;

						margin-bottom: 45px;

						& > div {
							@include make-col(2);

							img {
								width: 100%;
							}
						}

						& > p {
							display: inline-block;
							@include make-col()
						}
					}

					&_buttons {
						display: flex;
						justify-content: flex-start;

						button {
							padding-right: 50px;
							padding-left: 50px;

							&:not(:last-child) {
								margin-right: 10px;
							}
						}
					}

					&_button-close {
					}

					.input-domain__field {
						display: flex;
						align-items: center;
						position: relative;

						input {
							width: 100%;
							background-color: #e6e6e9;
							padding-right: 160px;
						}

						span {
							position: absolute;
							top: 0;
							right: 0;

							height: 100%;
							padding: 0 45px;
							line-height: 45px;
							background-color: #6666cc;
							color: $white;
						}
					}

				}
			}

			@include media-breakpoint-down(lg) {
				position: fixed;

				top: 50%;

				left: 50%;

				transform: translate(-50%, -50%);

			}

			@include media-breakpoint-down(md) {

				top: 50%;
				left: 0;
				right: 0;

				transform: translateY(-50%);

				max-width: 100%;

			}

			@include media-breakpoint-down(sm) {
				padding-left: 0;
				padding-right: 0;
				top: 0;
				bottom: 0;
				left: 0;
				right: 0;
				width: 100%;
				transform: none;
				max-width: none;
				.popup {
					&__setting {
						&_select {
							flex-wrap: wrap;

							label {
								@include make-col(12);

								&:not(:last-child) {
									margin-bottom: 55px;
								}
							}
						}

						.input-domain__field {
							input {
								@include media-breakpoint-down(xs) {
									padding-right: 100px;
								}
							}

							span {
								padding: 0 15px;
							}
						}

						&_attention {
							text-align: center;

							& > div {
								display: none;
							}
						}

						&_buttons {
							flex-wrap: wrap;
							justify-content: space-between;

							button {
								@include make-col(12);

								&:not(:last-child) {
									margin-bottom: 15px;
								}
							}
						}
					}
				}

			}

		}
	}

</style>


