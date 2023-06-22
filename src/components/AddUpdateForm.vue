<script setup>
import { ref, reactive } from 'vue';


const emit = defineEmits(['close-form', 'add-new-event'])

const newEvent = reactive({
	// event: '',
	// details: '',
	// date: '',
	// background: ''
})

function addEvent() {
	emit('add-new-event', newEvent) 
	emit('close-form')
}

// Data Validation

const errors = ref([])

function validate() {
	if (!newEvent.name) errors.value.push('Name is required')
	if (!newEvent.details) errors.value.push('Details is required')
	if (!newEvent.date) errors.value.push('Date is required')
	if (!newEvent.background) errors.value.push('Background is required')
	
	// Don't add event if there are errors
	if (errors.value.length > 0) return

	// Add event to newEvent array if there are no errors
	addEvent()
}


</script>
<template>
    <div class="form_wrapper">
      <form
				@keyup.enter.prevent="validate()"
				>
				<div v-if="errors.length > 0">
					<ul>
						<li v-for="error in errors">
							{{ error }}
						</li>
					</ul>
				</div>
				<span @click="emit('close-form')">&#10060</span>
        <div>
          <label for="name">Event:</label>
          <input type="text" id="name" v-model="newEvent.name" />
        </div>
        <div>
          <label for="details">Details:</label>
          <input type="text" id="details" v-model="newEvent.details"  />
        </div>
        <div>
          <label for="date">Date:</label>
          <input type="date" id="date" v-model="newEvent.date"/>
        </div>
        <div>
          <label for="background">Background:</label>
          <select id="background" v-model="newEvent.background">
            <option value="#F34949">Red</option>
            <option value="#F07AEC">Pink</option>
            <option value="#997AF0">Purple</option>
            <option value="#7AD3F0">Blue</option>
            <option value="#68EE94">Green</option>
            <option value="#f9f970">Yellow</option>
            <option value="#EB9A0F">Orange</option>
          </select>
        </div>
        <div>
          <button @click.prevent="validate()">add</button>
        </div>
      </form>
    </div>
  </template>

<style lang="scss" scoped>
.form_wrapper {
    background: rgba(0, 0, 0, 0.7);
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

form {
		display: flex;
		flex-direction: column;
    background-color: white;
    min-width: 40vw;
    min-height: 60vh;
    padding: 2rem;
    border-radius: 0.3rem;
   

    div {
        display: flex;
        flex-direction: column;
        margin: 1rem 0;
        font-size: 1.6rem;
    }

    input, 
    select {
        margin: 0.5rem;
        padding: 0.6rem 1rem;
        border: 1px lightgray solid;
        border-radius: 0.3rem;
    }

    button {
        background: rgb(123, 194, 123);
        width: 100px;
        border: none;
        padding: 0.6rem;
        border-radius: 0.3rem;
        font-size: 16px;
        align-self: center;
				cursor: pointer;
    }

    label {
        color: rgb(49, 49, 49);
        align-self: center;
    }
    
		span {
			align-self: flex-end;
			cursor: pointer;
		}
}

</style>