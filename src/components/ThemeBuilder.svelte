<script>
  import UIPreviewSVG from "./UIPreviewSVG.svelte";
  import ColorInput from "./ColorInput.svelte";

  let aubergine = [
    "#3F0E40",
    "#350d36",
    "#1164A3",
    "#FFFFFF",
    "#350D36",
    "#FFFFFF",
    "#2BAC76",
    "#CD2553"
  ];
  let nocturne = [
    "#1A1D21",
    "#000000",
    "#0576B9",
    "#FFFFFF",
    "#000000",
    "#FFFFFF",
    "#39E500",
    "#CC4400"
  ];

  let colors;
  $: colors = nocturne;
  $: encodedColors = encodeURIComponent(String(colors));

  let urlParams = new URLSearchParams(window.location.search);
  let hasColorsParam = urlParams.has("colors");

  const updateQueryStringParam = (key, value) => {
    let baseUrl = [
      location.protocol,
      "//",
      location.host,
      location.pathname
    ].join("");
    let newParam = key + "=" + value;
    let params = "?" + newParam;
    window.history.replaceState({}, "", baseUrl + params);
    console.log(`Colors from input: ${colors}`);
  };

  let URLHasBeenRead = false;

  const readQueryStringParam = () => {
    if (!URLHasBeenRead) {
      let colorParams = urlParams.get("colors");
      let newColorArray = colorParams.split(",");
      colors = newColorArray;
      URLHasBeenRead = true;
      console.log(`Colors from URL: ${colors}`);
    } else {
      colors = colors;
      updateQueryStringParam("colors", encodedColors);
    }
  };

  // DO STUFF HERE
  $: if (hasColorsParam) {
    readQueryStringParam();
  } else {
    updateQueryStringParam("colors", encodedColors);
  }
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
    inputId="columnBG"
    bind:value={colors[0]} />

  <ColorInput
    inputLabel="Menu BG Hover"
    inputId="menuBGHover"
    bind:value={colors[1]} />

  <UIPreviewSVG
    columnBG={colors[0]}
    menuBGHover={colors[1]}
    activeItem={colors[2]}
    activeItemText={colors[3]}
    hoverItem={colors[4]}
    textColor={colors[5]}
    activePresence={colors[6]}
    mentionBadge={colors[7]} />
</div>
