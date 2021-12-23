<template>
	<form class="form">
		<h3>Добавить клиента</h3>
		<div class="form__section">
			<div class="form__item">
				<label for="surname" class="form__label">Фамилия</label>
				<input type="text" class="form__control" id="surname" />
			</div>
			<div class="form__item">
				<label for="name" class="form__label">Имя</label>
				<input type="text" class="form__control" id="name" />
			</div>
			<div class="form__item">
				<label for="patronymic" class="form__label">Отчество</label>
				<input type="text" class="form__control" id="patronymic" />
			</div>
			<div class="form__item">
				<label for="dob" class="form__label">Дата рождения</label>
				<input type="date" class="form__control" id="dob" />
			</div>
			<div class="form__item">
				<label for="phone" class="form__label">Номер телефона</label>
				<input type="text" class="form__control" id="phone" />
			</div>
			<div class="form__item form__item--radio">
				<label class="form__label">Пол</label>
				<div class="form__radio">
					<label for="male" class="form__label">Мужской</label>
					<input
						type="radio"
						class="form__control"
						name="sex"
						id="male"
					/>
					<label for="female" class="form__label">Женский</label>
					<input
						type="radio"
						class="form__control"
						name="sex"
						id="female"
					/>
				</div>
			</div>
			<div class="form__item">
				<label for="customer-group" class="form__label"
					>Группа клиентов</label
				>
				<input type="text" class="form__control" id="customer-group" />
			</div>
			<div class="form__item">
				<label for="therapist" class="form__label">Лечащий врач</label>
				<input type="text" class="form__control" id="therapist" />
			</div>
			<div class="form__item form__item--checkbox">
				<label for="sms" class="form__label">Не отправлять СМС</label>
				<div class="form__checkbox">
					<input type="checkbox" class="form__control" id="sms" />
				</div>
			</div>
		</div>

		<h3>Адрес</h3>
		<div class="form__section">
			<div class="form__item">
				<label for="index" class="form__label">Индекс</label>
				<input type="text" class="form__control" id="index" />
			</div>
			<div class="form__item">
				<label for="country" class="form__label">Страна</label>
				<input type="text" class="form__control" id="country" />
			</div>
			<div class="form__item">
				<label for="region" class="form__label">Область</label>
				<input type="text" class="form__control" id="region" />
			</div>
			<div class="form__item">
				<label for="city" class="form__label">Город</label>
				<input type="text" class="form__control" id="city" />
			</div>
			<div class="form__item">
				<label for="street" class="form__label">Улица</label>
				<input type="text" class="form__control" id="street" />
			</div>
			<div class="form__item">
				<label for="house" class="form__label">Дом</label>
				<input type="text" class="form__control" id="house" />
			</div>
		</div>

		<h3>Документ</h3>
		<div class="form__section">
			<div class="form__item">
				<label for="doc-type" class="form__label">Тип документа</label>
				<input type="text" class="form__control" id="doc-type" />
			</div>
			<div class="form__item">
				<label for="series" class="form__label">Серия</label>
				<input type="text" class="form__control" id="series" />
			</div>
			<div class="form__item">
				<label for="number" class="form__label">Номер</label>
				<input type="text" class="form__control" id="number" />
			</div>
			<div class="form__item">
				<label for="issued-by" class="form__label">Кем выдан</label>
				<input type="text" class="form__control" id="issued-by" />
			</div>
			<div class="form__item">
				<label for="date-of-issue" class="form__label"
					>Дата выдачи</label
				>
				<input type="date" class="form__control" id="date-of-issue" />
			</div>
		</div>

		<div class="form__section">
			<button class="form__btn">Добавить клиента</button>
		</div>
	</form>
</template>

<script>
export default {
	name: 'Form',
};
</script>

<style lang="scss">
.form {
	margin: 0 auto;
	padding: 20px;
	max-width: 1024px;
	box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.2);
	border-radius: 4px;
	& h3 {
		margin: 0 0 8px 10px;
	}
	&__section {
		display: flex;
		flex-wrap: wrap;
		justify-content: space-between;
		margin-bottom: 15px;
		&:last-child {
			margin-bottom: 0;
			justify-content: end;
		}
	}
	&__item {
		display: flex;
		flex-direction: column;
		flex: 1 250px;
		padding: 10px;
		min-height: 74px;
		&--checkbox input {
			width: 20px;
			height: 20px;
			margin: 0;
			position: relative;
			&:checked::before {
				content: '';
				position: absolute;
				top: 6px;
				left: 6px;
				right: 4px;
				bottom: 6px;
				// background: transparent;
				border-bottom: 2px solid #8ba4f9;
				border-right: 2px solid #8ba4f9;
				transform: rotate(45deg) translate(-2px);
				z-index: 1;
			}
			&:checked::after {
				content: '';
				position: absolute;
				top: -1px;
				left: -1px;
				right: -1px;
				bottom: -1px;
				background: #fff;
				border: 2px solid #bc9cff;
				border-radius: 4px;
			}
		}
	}
	&__label {
		font-weight: bold;
		font-size: 12px;
		text-transform: uppercase;
		color: #1f2041;
	}
	&__control {
		border: 1px solid rgba(31, 32, 65, 0.25);
		height: 100%;
		border-radius: 4px;
		margin-top: 5px;
		padding: 8px;
		outline: none;
		transition: 0.2s ease-in-out border;
		&:hover,
		&:focus,
		&:active {
			border: 1px solid rgba(31, 32, 65, 0.5);
		}
	}
	&__radio {
		display: flex;
		align-items: center;
		height: 100%;
		& label {
			font-weight: normal;
		}
		& input {
			width: 20px;
			height: 20px;
			margin: 0 15px 0 5px;
			position: relative;
			&:checked::before {
				content: '';
				position: absolute;
				top: 0;
				left: 0;
				right: 0;
				bottom: 0;
				border: 1px solid #bc9cff;
				border-radius: 50%;
				background: #fff;
			}
			&:checked:after {
				content: '';
				position: absolute;
				border: 1px solid #bc9cff;
				border-radius: 50%;
				top: 4px;
				left: 4px;
				right: 4px;
				bottom: 4px;
				background: linear-gradient(180deg, #bc9cff 0%, #8ba4f9 100%);
			}
		}
	}
	&__checkbox {
		display: flex;
		align-items: center;
		height: 100%;
	}
	&__btn {
		margin-right: 10px;
		background: linear-gradient(180deg, #bc9cff 0%, #8ba4f9 100%);
		border: none;
		border-radius: 22px;

		color: #fff;
		font-size: 12px;
		font-weight: bold;
		text-transform: uppercase;
		padding: 14px 21px;

		transition: 0.2s ease-in-out opacity;
		&:hover {
			opacity: 0.5;
		}
	}
}
</style>
