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

  let colors = [...nocturne];

  const updateQueryStringParam = (key, value) => {
    var baseUrl = [
        location.protocol,
        "//",
        location.host,
        location.pathname
      ].join(""),
      urlQueryString = document.location.search,
      newParam = key + "=" + value,
      params = "?" + newParam;

    window.history.replaceState({}, "", baseUrl + params);
  };
  $: updateQueryStringParam("colors", encodeURIComponent(String(colors)));

  const urlParams = new URLSearchParams(window.location.search);
  console.log(`has colors ${urlParams.has("colors")}`); // true
  console.log(`colors: ${urlParams.get("colors")}`); // "shirt"

  // console.log(typeof colorsAsString);
  // console.log(colorsAsString);
  // console.log(encodedColors);

  $: console.log(colors);

  // updateQueryStringParam("colors", encodedColors);
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
