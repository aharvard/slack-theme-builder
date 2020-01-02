<script>
  export let inputLabel = "label";
  export let id = "id";
  export let value = "#333";
</script>

<label for={id}>{inputLabel}</label>
<input type="text" name={id} id bind:value />
