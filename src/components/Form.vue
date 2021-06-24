<template>
	<form @submit.prevent="submitForm">
		<input type="number" v-model.number="degree" required />

		<select id="selectedTemp" name="selectedTemp" v-model="selectedTemp" required>
			<option disabled value="">-- Select Temperature --</option>
			<option value="celcius">Celcius</option>
			<option value="fahrenheit">Fahrenheit</option>
		</select>

		<button>Convert</button>
	</form>

	<ShowResult :result="result"/>
</template>

<script>
import ShowResult from './ShowResult.vue'

export default {
	components: { ShowResult },
	data() {
		return {
			degree: null,
			selectedTemp: '',
			result: null
		}
	},
	methods: {
		submitForm(e) {
			// convert Celcius to Fahrenheit
			const toFahrenheit = (this.degree * 9) / 5 + 32

			// convert Fahrenheit to Celcius
			const toCelcius = (this.degree - 32) * 5 / 9

			// convert based on selected temperature
			if(this.selectedTemp === 'celcius') {
				this.result = `${Math.round(parseFloat(toFahrenheit))} Fahrenheit`
			} else if(this.selectedTemp === 'fahrenheit') {
				this.result = `${Math.round(parseFloat(toCelcius))} Celcius`
			}

			this.clearForm()
		},
		// clear the inputs after submit
		clearForm() {
			this.degree = null
			this.selectedTemp = ''
		}
	},
}
</script>
