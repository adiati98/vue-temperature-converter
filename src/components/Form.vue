<template>
	<form @submit.prevent="submitForm">
		<label for="degree">Degree: </label>
		<input type="number" v-model.number="degree" />
		<label for="selectedTemp">Temperature: </label>
		<select id="selectedTemp" name="selectedTemp" v-model="selectedTemp" required>
			<option value="celcius">Celcius</option>
			<option value="fahrenheit">Fahrenheit</option>
		</select>

		<button>{{ btnText }}</button>
	</form>

	<ShowResult :result="result" />
</template>

<script>
import ShowResult from './ShowResult.vue'

export default {
	components: { ShowResult },
	data() {
		return {
			degree: null,
			selectedTemp: 'celcius',
			result: null,
			btnText: 'Convert',
		}
	},
	methods: {
		submitForm(e) {
			// degree field has to be filled
			if (this.degree === null && this.btnText === 'Convert') {
				this.result = 'Please enter required field'
				// convert when degree input is filled and result is null
			} else if (this.result === null || this.degree !== null) {
				this.convertion()
				this.clearInputs()
				// reset form
			} else if (this.result !== null) {
				this.clearForm()
			} 
		},
		convertion() {
			// convert Celcius to Fahrenheit
			const toFahrenheit = (this.degree * 9) / 5 + 32

			// convert Fahrenheit to Celcius
			const toCelcius = ((this.degree - 32) * 5) / 9

			// convert based on selected temperature
			if (this.selectedTemp === 'celcius') {
				this.result = `${Math.round(parseFloat(toFahrenheit))} Fahrenheit`
			} else if (this.selectedTemp === 'fahrenheit') {
				this.result = `${Math.round(parseFloat(toCelcius))} Celcius`
			}
		},
		// clear the inputs after submit
		clearInputs() {
			this.degree = null
			this.selectedTemp = 'celcius'
			this.btnText = 'Reset'
		},
		// reset form
		clearForm() {
			this.result = null
			this.btnText = 'Convert'
		},
	},
}
</script>
