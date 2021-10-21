<script>
let ratings =  [1,2,3,4,5,6,7,8,9,10]
</script>

<div class="radio-toolbar">
    {#each ratings as rating (rating)}
      <input type="radio" id="num{rating}" name="rating" value="{rating}" checked>
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
    border: 2px solid #444;
    border-radius: 50%;
    text-align: center;
    margin: 5px
}

.radio-toolbar label:hover {
  background-color: #dfd;
}

.radio-toolbar input[type="radio"]:focus + label {
    border: 2px dashed #444;
}

.radio-toolbar input[type="radio"]:checked + label {
    background-color: #bfb;
    border-color: #4c4;
}


</style>