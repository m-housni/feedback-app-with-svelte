<script>

// import modules
import {createEventDispatcher} from 'svelte' // responsible for dispatching events between the app components, imported from node_modules/svelte/inndex.js
const dispatch = createEventDispatcher() // so we can say: dispatch('event-name', value)
import {v4 as uuidv4} from 'uuid' // helps in creating unique identifiers

// import components
import RatingSelect from './RatingSelect.svelte'

// set variables
let btnDisabled = true // tells if the button should be disabled
let error = null // tells if an error message should be displayed
let rating = null // sets the initial rating value
let text = '' // sets the initial text value
let min = 5 // minimum number of input chars

// define functions
const handleInput = (e) => {
  // 
  let ln = e.target.value.trim().length
  if(ln>=min) {
    btnDisabled = false
    error = null
    text = e.target.value
  } else {
    btnDisabled = true
    error = 'Min '+min+' chars'
  }
}

const handleSelect = (e) => {
  rating = e.detail
}

const handleSubmit = () => {
  // validation
  if(!rating) {
    alert('Please rate!')
    return
  }

  // new feedback
  const newFeedback = {
    id: uuidv4(),
    text: text,
    rating: +rating
  }

  // push new feedback to feedbacks
  dispatch('new-feedback',newFeedback)
  text = ''
  
}

</script>

<form on:submit|preventDefault={handleSubmit}>
  <RatingSelect on:rating-select={handleSelect} />
  <div class="input-group text-center">
    <input type="text" value={text} placeholder="Feedback" on:input={handleInput}>
    <button type="submit" disabled={btnDisabled}>Send</button>
  </div>
  {#if error}
    <span class="error-badge">{error}</span>
  {/if}
</form>

<style>

  .error-badge {
    background: #fff;
    color: red;
    padding: 5px 15px;
    border: 1px #1E1D37 solid;
    border-radius: 10px;
    font-size:.8rem;
    margin-left: 10px;

  }

  form {
    background: #fff;
    padding: 50px 50px;
    margin: 15px;
    border-radius: 15px;
  }

  .input-group {
    border-radius: 15px;
    border: 1px lightgray solid;
    background: #fff;
    padding: 10px;
  }

  input {
    min-width: 75%;
    border: none;
    padding: 8px;
    margin: 0;
  }

  input:focus {
    outline: none;
  }

  button {
    padding: 5px 10px;
    border-radius: 10px;
    width: 20%;
    float: right;
    background: #1E1D37;
    color: #fff;
  }
</style>