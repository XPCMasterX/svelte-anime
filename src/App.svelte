<script>
  import anime from "animejs/lib/anime.es.js";
  import { fade } from "svelte/transition";
  let x1 = 10;
  let y = 50;
  let x2 = 190;
  let sw = 1;
  let showText = false;
  let stroke_line2 = "transparent";
  let stroke_line = "transparent";
  function test() {
    let x = document.querySelector(".line");
    stroke_line = "white";
    let lineExpand = anime({
      targets: x,
      ["x2"]: [100, 190],
      ["x1"]: [100, 10],
      easing: "easeInOutExpo",
    });
    lineExpand.finished.then(() => {
      stroke_line2 = "white";
      let top = anime({
        targets: ".line",
        ["y1"]: [50, 10],
        ["y2"]: [50, 10],
        easing: "easeInOutExpo",
      });
      let bottom = anime({
        targets: ".line2",
        ["y1"]: [50, 90],
        ["y2"]: [50, 90],
        easing: "easeInOutExpo",
      });
      Promise.all([top.finished, bottom.finished]).then(() => {
        showText = true;
      });
    });
  }
</script>

<main>
  <svg width="500" height="500" viewbox="0 0 200 200">
    <line
      class="line"
      stroke={stroke_line}
      stroke-width={sw}
      {x1}
      {x2}
      y1={y}
      y2={y}
    />
    {#if showText}
      <text
        transition:fade
        x="23"
        y="67.5"
        font-family="Roboto"
        fill="white"
        font-size="3em"
        font-weight="100">MAYBE</text
      >
    {/if}
    <line
      class="line2"
      stroke={stroke_line2}
      stroke-width={sw}
      {x1}
      {x2}
      y1={y}
      y2={y}
    />
  </svg>
  <button on:click={test}> click</button>
</main>

<style>
</style>
