<script setup>
import { computed } from 'vue';

    
const props = defineProps({
	event: {
		type: Object,
	},
	daysLeft: {
		type: Number
	},
	showPastEvents: Boolean,

}) 

// Function
// function daysLeftString() {
// 	const dayOrDays = Math.abs(props.daysLeft) === 1 ? 'day' : 'days' 
// 	const leftOrAgo = Math.sign(props.daysLeft) != -1 ? 'left' : 'ago'
// 	return `${dayOrDays} ${leftOrAgo}`
// }

// Computed
const daysLeftString = computed(() => {
	const dayOrDays = Math.abs(props.daysLeft) === 1 ? 'day' : 'days' 
	const leftOrAgo = Math.sign(props.daysLeft) != -1 ? 'left' : 'ago'
	return `${dayOrDays} ${leftOrAgo}`
})

const changeContrast = computed(() => {
	const lowContrastBackgrounds = ['#f9f970', '#68EE94']
	return lowContrastBackgrounds.includes(props.event.background)
})

</script>

<template>
     <article 
		 v-show=" Math.sign(daysLeft) !== -1 || showPastEvents "
		 :style="{ 
				backgroundColor : event.background,
				color: changeContrast ? '#454444' : 'whitesmoke' 
			}"
		>
				<div class="data">
					<h3 class="name">{{ event.name }}!</h3>
					<p class="details">{{ event.details }}</p>
				</div>
				<div class="countdown">
					<div class="remove_btn_wrapper">
						<button class="remove_btn">&#10060;</button>
					</div>
					<p v-if="daysLeft === 0">Today</p>
					<p v-else>
						{{ Math.abs(daysLeft) }}
						
						<br />
						<!-- Function Call -->
						<!-- <small>{{ daysLeftString() }}</small> -->
						
						<!-- Computed Call - this is better for updating data because you don't have to call a function, which requires a browser refresh-->
						<small>{{ daysLeftString }}</small>
					</p>
				</div>
			</article>
</template>



<style lang="scss" scoped>
article {
	background: lightslategray;
  display: flex;
  align-items: center;
  border-radius: 1rem;
  margin: 1rem 0;
  padding: 0.2rem 1rem;
  color: whitesmoke;
  font-weight: 300;
	justify-content: space-around;

	 .data{
		flex: 3;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		.name{
			font-size: 1.8rem;
		}
		.details{
			font-size: 1.6rem;
		}
	 }
	 .countdown {
		flex: 1;
		text-align: center;
		font-size: 1.6rem;
		border-left: 1px solid;

		.remove_btn_wrapper {
			text-align: right;
			.remove_btn{
			background-color: transparent;
			border: none;
			cursor: pointer;
			
		}
		}

	 }
}

</style>