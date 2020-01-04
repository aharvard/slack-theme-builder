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

  $: colors = aubergine;
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
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    place-items: center;
  }
  @media (min-width: 50em) {
    .theme-builder {
      grid-template-columns: auto 1fr;
    }
  }

  .color-inputs {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
  }

  .ui-preview-svg {
    width: 100%;
  }
</style>

<h2>Theme Builder</h2>
<div class="theme-builder">
  <form class="color-inputs">
    <ColorInput
      inputLabel="Column BG"
      inputId="columnBG"
      bind:value={colors[0]} />

    <ColorInput
      inputLabel="Menu BG Hover"
      inputId="menuBGHover"
      bind:value={colors[1]} />

    <ColorInput
      inputLabel="Active Item"
      inputId="activeItem"
      bind:value={colors[2]} />

    <ColorInput
      inputLabel="Active Item Text"
      inputId="activeItemText"
      bind:value={colors[3]} />

    <ColorInput
      inputLabel="Hover Item"
      inputId="hoverItem"
      bind:value={colors[4]} />

    <ColorInput
      inputLabel="Text Color"
      inputId="textColor"
      bind:value={colors[5]} />

    <ColorInput
      inputLabel="Active Presence"
      inputId="activePresence"
      bind:value={colors[6]} />

    <ColorInput
      inputLabel="Mention Badge"
      inputId="mentionBadge"
      bind:value={colors[7]} />
  </form>
  <div class="ui-preview-svg">
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
</div>

<div>
  <h2>Paste These Into Slack</h2>
  <p>{colors}</p>
</div>
