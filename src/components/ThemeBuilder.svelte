<script>
  import UIPreviewSVG from "./UIPreviewSVG.svelte";
  import ColorInput from "./ColorInput.svelte";

  let themeColors = {
    columnBG: "red",
    menuBGHover: "#ffa300",
    activeItem: "#ffa300",
    activeItemText: "#ffffff",
    hoverItem: "#ffc25f",
    textColor: "#d6d6d6",
    activePresence: "#ffa300",
    mentionBadge: "#c97c00"
  };
</script>

<style>
  .theme-builder {
    outline: 1px solid gainsboro;
  }
</style>

<div class="theme-builder">
  <h2>Theme Builder</h2>

  <ColorInput
    inputLabel="Column BG"
    id="columnBG"
    bind:value={themeColors.columnBG} />

  <ColorInput
    inputLabel="Text Color"
    id="textColor"
    bind:value={themeColors.textColor} />

  <!-- {#each themeColorsArray as color} -->
  <!-- <ul> -->
  <!-- <li>{color}</li> -->
  <!-- </ul> -->
  <!-- {/each} -->

  <UIPreviewSVG {themeColors} />
</div>
