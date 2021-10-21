<script>

let btnDisabled = true

const handleInput = (e) => {
  let ln = e.target.value.trim().length
  if(ln>=10) {
    btnDisabled = false
  } else {
    btnDisabled = true
  }
}

$: error = btnDisabled ? 'Min 10 chars' : false

</script>

<form>
  <div class="input-group text-center">
    <input type="text" placeholder="Feedback" on:input={handleInput}>
    <button disabled={btnDisabled}>Send</button>
  </div>
  {#if error}<span class="error-badge">{error}</span>{/if}
</form>

<style>

  .error-badge {
    background: #fff;
    color: red;
    padding: 5px 15px;
    border: 1px purple solid;
    border-radius: 10px;
    font-size:.8rem;
    margin-left: 10px;

  }

  form {
    background: purple;
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