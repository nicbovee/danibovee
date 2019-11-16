<script>
  import { onMount } from "svelte";

  export let name;
  let danibovee = "dani bovee.".split("");
  let daniobj = danibovee.map(x => ({
    letter: x,
    color: "#000",
    size: 18
  }));
  let background = "danibovee".split("");

  let i = 0;
  let maxLetterCount = 4000;
  let letterArray = [];
  while (i < maxLetterCount) {
    letterArray.push({
      letter:
        i % 2 === 0
          ? " "
          : background[getRandomArbitrary(0, background.length - 1)],
      color: getRandomColor(0.3),
      size: 32
    });
    i++;
  }
  function clickme(isRandom = true, size) {
    daniobj = danibovee.map(x => {
      return {
        letter: x,
        color: getRandomColor(),
        size: isRandom ? getRandomArbitrary(15, 200) : size
      };
    });

    // danibovee.split('').forEach(x => {
    //     var r = Math.round((Math.random() * 254));
    //     var g = Math.round((Math.random() * 254));
    //     var b = Math.round((Math.random() * 254));
    //     var newSpan = document.createElement('span');
    //     newSpan.textContent = x;
    //     newSpan.style.fontSize = getRandomArbitrary(15, 200);
    //     newSpan.style.color = `rgb(${r},${g},${b})`;
    //     dani.appendChild(newSpan);
    // })
  }
  function getRandomColor(opacity) {
    let r = Math.round(Math.random() * 254);
    let g = Math.round(Math.random() * 254);
    let b = Math.round(Math.random() * 254);
    return opacity ? `rgba(${r},${g},${b},${opacity})` : `rgb(${r},${g},${b})`;
  }
  function getRandomArbitrary(min, max) {
    return Math.round(Math.random() * (max - min) + min);
  }

  function test() {
    letterArray = letterArray.map((x, i) => ({
      letter:
        i % 2 === 0
          ? " "
          : background[getRandomArbitrary(0, background.length - 1)],
      color: getRandomColor(0.3),
      size: 32
      // if(x.letter !== " "){
      //   x.color = getRandomColor()
      //   console.log(x);
      // }
    }));
  }
  onMount(() => {
    const interval = setInterval(() => {
      test();
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  });
</script>

<style>
  main {
    background: #fff0cd;
  }
  #wrapper {
    position: fixed;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 1em;
    margin: 0 auto;
    width: 100%;
    height: 100%;
    -webkit-touch-callout: none; /* iOS Safari */
    -webkit-user-select: none; /* Safari */
    -khtml-user-select: none; /* Konqueror HTML */
    -moz-user-select: none; /* Old versions of Firefox */
    -ms-user-select: none; /* Internet Explorer/Edge */
    user-select: none;
    overflow: hidden;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  #dani {
    text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.4);
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main on:click={clickme}>

  <div id="wrapper">
    <div id="dani">
      {#each daniobj as obj, i (i)}
        <span style="font-size: {obj.size}px; color: {obj.color}">
          {obj.letter}
        </span>
      {/each}
    </div>
  </div>
  {#each letterArray as obj, i (i)}
    <span style="font-size: {obj.size}px; color: {obj.color}">
      {obj.letter}
    </span>
  {/each}
</main>
