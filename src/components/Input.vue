<template>
	<div v-if="type === 'radio'" class="form__item form__item--radio">
		<label v-show="title" class="form__label">{{ title }}</label>
		<div class="form__radio">
			<div
				style="display: flex; align-items: center"
				v-for="radio in radioButtons"
				:key="radio.id"
			>
				<label :for="radio.id" class="form__label">{{
					radio.title
				}}</label>
				<input
					type="radio"
					class="form__control"
					:name="radioName"
					:id="radio.id"
					:value="radio.title"
					@input="$emit('update:value', $event.target.value)"
				/>
			</div>
		</div>
		<small class="inputMessage" :class="{ show: valid.valid }">{{
			valid.error
		}}</small>
	</div>

	<div
		v-else-if="type === 'multiSelect'"
		class="form__item form__item--checkbox form__item--multiselect"
	>
		<label v-show="title" class="form__label">{{ title }}</label>
		<p
			class="form__control"
			style="margin-bottom: 0"
			@click="showSelect = !showSelect"
		>
			{{ multiFiltered }} <span>&#9660;</span>
		</p>
		<div :class="{ show: showSelect }" class="multiselect__options">
			<label v-for="checkbox in checkboxes" :key="checkbox.id">
				<input
					type="checkbox"
					class="form__control"
					:name="checkbox.name"
					:value="checkbox.name"
					:id="checkbox.id"
					v-model="multi"
					@change="$emit('update:value', multi)"
				/>{{ checkbox.name }}
			</label>
		</div>
		<small class="inputMessage" :class="{ show: valid.valid }">{{
			valid.error
		}}</small>
	</div>

	<div
		v-else-if="type === 'select'"
		class="form__item form__item--checkbox form__item--multiselect"
	>
		<label v-show="title" class="form__label">{{ title }}</label>
		<p
			class="form__control"
			style="margin-bottom: 0"
			@click="showSelect = !showSelect"
		>
			{{ selFiltered }} <span>&#9660;</span>
		</p>
		<div :class="{ show: showSelect }" class="multiselect__options">
			<label
				v-for="option in selectOptions"
				:key="option.id"
				@click="
					sel = option.name;
					$emit('update:value', selFiltered);
				"
				:class="{ selected: selFiltered === option.name }"
			>
				{{ option.name }}
			</label>
		</div>
		<small class="inputMessage" :class="{ show: valid.valid }">{{
			valid.error
		}}</small>
	</div>

	<div v-else class="form__item">
		<label v-show="title" :for="id" class="form__label">{{ title }}</label>
		<input
			:type="type"
			class="form__control"
			:id="id"
			:value="value"
			@input="$emit('update:value', $event.target.value)"
		/>
		<small class="inputMessage" :class="{ show: valid.valid }">{{
			valid.error
		}}</small>
	</div>
</template>

<script>
export default {
	name: 'Input',
	props: {
		title: {
			type: String,
			default: '',
		},
		type: {
			type: String,
			default: 'text',
		},
		id: {
			type: String,
			default: '',
		},
		placeholder: {
			type: String,
			default: 'Выбрать',
		},
		radio: {
			type: Array,
		},
		value: {
			type: [String, Number, Array],
		},
		radioName: {
			type: String,
			default: '',
		},
		radioButtons: {
			type: Array,
		},
		selectOptions: {
			type: Array,
		},
		checkboxes: {
			type: Array,
		},
		valid: {
			type: Object,
			default() {
				return {
					valid: true,
					error: '',
				};
			},
		},
	},
	data() {
		return {
			selectValue: 0,
			showSelect: false,
			multi: [],
			sel: '',
		};
	},
	methods: {
		openSelect() {},
	},
	computed: {
		multiFiltered() {
			return this.multi.length > 0
				? this.multi.join(', ')
				: this.placeholder;
		},
		selFiltered() {
			return this.sel ? this.sel : this.placeholder;
		},
	},
};
</script>

<style lang="scss">
.form__item {
	&--multiselect {
		position: relative;
		& p {
			display: flex;
			align-items: center;
			justify-content: space-between;
			font-size: 12px;
		}
	}
}

.multiselect__options {
	display: none;
	border: 1px solid rgba(31, 32, 65, 0.25);
	margin-top: 5px;
	border-radius: 4px;
	position: absolute;
	top: 85%;
	left: 10px;
	right: 10px;
	background: #fff;
	box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.2);
	z-index: 2;
	& label {
		font-size: 12px;
		&:hover {
			background: linear-gradient(180deg, #bc9cff 0%, #8ba4f9 100%);
			color: #fff;
		}
		& input {
			margin-right: 5px;
		}
		display: flex;
		align-items: center;
		margin: 0;
		padding: 6px;
		border-bottom: 1px solid rgba(31, 32, 65, 0.25);
		&:last-child {
			border-bottom: none;
		}
	}
}
.inputMessage {
	display: none;
	color: red;
}
.show {
	display: block;
}
.selected {
	background: linear-gradient(180deg, #bc9cff 0%, #8ba4f9 100%);
	color: #fff;
}
</style>
