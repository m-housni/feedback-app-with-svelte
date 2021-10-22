<script>
import {createEventDispatcher} from 'svelte'
const dispatch = createEventDispatcher()
let ratings =  [1,2,3,4,5,6,7,8,9,10]

const onChange = (e) => {
  dispatch('rating-select', e.currentTarget.value)
}
</script>

<div class="radio-toolbar">
    {#each ratings as rating (rating)}
      <input type="radio" id="num{rating}" name="rating" value="{rating}" on:change={onChange}>
      <label for="num{rating}">{rating}</label>
    {/each}
</div>
<p>&nbsp;</p>

<style>
.radio-toolbar {
  margin: 10px;
  text-align: center;
}

.radio-toolbar input[type="radio"] {
  opacity: 0;
  position: fixed;
  width: 0;
}

.radio-toolbar label {
    display: inline-block;
    background-color: #ddd;
    width: 20px;
    height: 20px;
    padding:10px;
    font-family: sans-serif, Arial;
    font-size: 20px;
    border: 2px solid #fff;
    border-radius: 50%;
    text-align: center;
    margin: 5px
}

.radio-toolbar label:hover {
  background-color: #dfd;
}

.radio-toolbar input[type="radio"]:focus + label {
    border: 2px solid #444;
}

.radio-toolbar input[type="radio"]:checked + label {
    background-color: #1E1D37;
    color: #fff;
    font-size: 20px;
}


</style>