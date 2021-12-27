<template>
	<form class="form" @submit.prevent="submitHandler">
		<h3>Добавить клиента</h3>
		<div class="form__section">
			<Input
				v-model:value="state.surname"
				title="Фамилия"
				id="surname"
				:valid="{
					valid: v$.surname.$error,
					error: v$.surname.$errors[0]
						? v$.surname.$errors[0].$message
						: '',
				}"
			/>
			<Input
				v-model:value="state.name"
				title="Имя"
				id="name"
				:valid="{
					valid: v$.name.$error,
					error: v$.name.$errors[0]
						? v$.name.$errors[0].$message
						: '',
				}"
			/>
			<Input title="Отчество" id="patronymic" />
			<Input
				v-model:value="state.dob"
				type="date"
				title="Дата рождения"
				id="dob"
				:valid="{
					valid: v$.dob.$error,
					error: v$.dob.$errors[0] ? v$.dob.$errors[0].$message : '',
				}"
			/>
			<Input
				v-model:value="state.phone"
				title="Номер телефона"
				id="phone"
				:valid="{
					valid: v$.phone.$error,
					error: v$.phone.$errors[0]
						? v$.phone.$errors[0].$message
						: '',
				}"
			/>
			<Input
				type="radio"
				title="Пол"
				:radioButtons="radioButtons"
				radioName="sex"
			/>
			<Input
				type="multiSelect"
				title="Группа клиентов"
				id="customer-group"
				v-model:value="state.selectedGroup"
				:checkboxes="clientGroup"
				:valid="{
					valid: v$.selectedGroup.$error,
					error: v$.selectedGroup.$errors[0]
						? v$.selectedGroup.$errors[0].$message
						: '',
				}"
			/>
			<Input type="select" title="Лечащий врач" :selectOptions="doctor" />
			<div class="form__item form__item--checkbox">
				<label for="sms" class="form__label">Не отправлять СМС</label>
				<div class="form__checkbox">
					<input type="checkbox" class="form__control" id="sms" />
				</div>
			</div>
		</div>

		<h3>Адрес</h3>
		<div class="form__section">
			<Input title="Индекс" id="index" />
			<Input title="Страна" id="country" />
			<Input title="Область" id="region" />
			<Input
				v-model:value="state.city"
				title="Город"
				id="city"
				:valid="{
					valid: v$.city.$error,
					error: v$.city.$errors[0]
						? v$.city.$errors[0].$message
						: '',
				}"
			/>
			<Input title="Улица" id="street" />
			<Input title="Дом" id="house" />
		</div>

		<h3>Документ</h3>
		<div class="form__section">
			<Input
				type="select"
				title="Тип документа"
				:selectOptions="document"
				v-model:value="state.docType"
				:valid="{
					valid: v$.docType.$error,
					error: v$.docType.$errors[0]
						? v$.docType.$errors[0].$message
						: '',
				}"
			/>
			<Input title="Серия" id="series" />
			<Input title="Номер" id="number" />
			<Input title="Кем выдан" id="issued-by" />
			<Input
				v-model:value="state.dateOfIssue"
				type="date"
				title="Дата выдачи"
				id="dateOfIssue"
				:valid="{
					valid: v$.dateOfIssue.$error,
					error: v$.dateOfIssue.$errors[0]
						? v$.dateOfIssue.$errors[0].$message
						: '',
				}"
			/>
		</div>

		<div class="form__section">
			<button class="form__btn" type="submit">Добавить клиента</button>
		</div>
	</form>
</template>

<script>
import Input from './Input.vue';

import { reactive, computed } from 'vue';
import useValidate from '@vuelidate/core';
import { required, minLength, helpers } from '@vuelidate/validators';

export default {
	name: 'Form',
	components: {
		Input,
	},
	setup() {
		const state = reactive({
			surname: '',
			name: '',
			dob: '',
			phone: '',
			selectedGroup: [],
			city: '',
			docType: '',
			dateOfIssue: '',
		});

		const validPhone = (val) => /^((7)+([0-9]){10})$/.test(val);

		const rules = computed(() => {
			return {
				surname: {
					required: helpers.withMessage('Введите Фамилию', required),
					minLength: helpers.withMessage(
						({ $params }) =>
							`Поле должно содержать минимум ${$params.min} символа!`,
						minLength(2)
					),
				},
				name: {
					required: helpers.withMessage('Введите имя', required),
					minLength: helpers.withMessage(
						({ $params }) =>
							`Поле должно содержать минимум ${$params.min} символа!`,
						minLength(2)
					),
				},
				dob: {
					required: helpers.withMessage(
						'Введите дату рождения',
						required
					),
				},
				phone: {
					validPhone: helpers.withMessage(
						'Введите номер в формате 79999999999',
						validPhone
					),
				},
				selectedGroup: {
					required: helpers.withMessage(
						'Поле не должно быть пустым',
						required
					),
				},
				city: {
					required: helpers.withMessage(
						'Поле не должно быть пустым',
						required
					),
				},
				docType: {
					required: helpers.withMessage(
						'Поле не должно быть пустым',
						required
					),
				},
				dateOfIssue: {
					required: helpers.withMessage(
						'Поле не должно быть пустым',
						required
					),
				},
			};
		});

		const v$ = useValidate(rules, state);

		return {
			state,
			v$,
		};
	},
	data() {
		return {
			multi: [],
			radioButtons: [
				{
					id: 1,
					title: 'Мужской',
					value: 'male',
				},
				{
					id: 2,
					title: 'Женский',
					value: 'female',
				},
			],
			doctor: [
				{
					id: 1,
					name: 'Иванов',
				},
				{
					id: 2,
					name: 'Захаров',
				},
				{
					id: 3,
					name: 'Чернышева',
				},
			],
			document: [
				{
					id: 1,
					name: 'Паспорт',
				},
				{
					id: 2,
					name: 'Свидетельство о рождении',
				},
				{
					id: 3,
					name: 'Вод. удостоверение',
				},
			],
			clientGroup: [
				{
					id: 1,
					name: 'VIP',
				},
				{
					id: 2,
					name: 'Проблемные',
				},
				{
					id: 3,
					name: 'ОМС',
				},
			],
		};
	},
	methods: {
		submitHandler() {
			this.v$.$validate();
			if (this.v$.$error) {
				console.log(this.v$.$errors);
				return;
			}
			alert('login');
		},
	},
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
		height: 40px;
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
