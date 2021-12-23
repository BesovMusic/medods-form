<template>
	<Form />
</template>

<script>
import Form from './components/Form.vue';

export default {
	name: 'App',
	components: {
		Form,
	},
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

* {
	font-family: 'Montserrat', sans-serif;
	box-sizing: border-box;
}
h1,
h2,
h3,
h4,
h5,
h6 {
	margin: 0;
}
</style>
