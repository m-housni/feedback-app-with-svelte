<script>
import {createEventDispatcher} from 'svelte'
const dispatch = createEventDispatcher()

import RatingSelect from './RatingSelect.svelte'
import {v4 as uuidv4} from 'uuid'
let btnDisabled = true, error = null
let rating = null
let text = ''

const handleInput = (e) => {
  let ln = e.target.value.trim().length
  if(ln>=10) {
    btnDisabled = false
    error = null
    text = e.target.value
  } else {
    btnDisabled = true
    error = 'Min 10 chars'
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
  }

  input {
    min-width: 75%;
    border: none;
    margin: 0;
  }

  input:focus {
    outline: none;
  }

  button {
    padding: 5px 10px;
    font-size: 10px;
    border-radius: 10px;
    width: 20%;
  }
</style>