<script>
  export let inputLabel = "Input label";
  export let inputId = "id";
  export let value = "#333";
</script>

<label for={inputId}>{inputLabel}</label>
<input id={inputId} type="text" name={inputId} bind:value />
