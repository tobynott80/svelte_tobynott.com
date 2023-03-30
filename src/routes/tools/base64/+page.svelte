<!-- Svelte componant to decode/encode base64 -->
<script>
  import { onMount } from "svelte";
  import { tick } from "svelte";

  let input = "";
  let output = "";

  function encode() {
    output = btoa(input);
  }

  function decode() {
    output = atob(input);
  }

  onMount(async () => {
    if (browser) {
      const inputEl = document.getElementById("input");
      const outputEl = document.getElementById("output");

      inputEl.addEventListener("input", (e) => {
        input = e.target.value;
        encode();
      });

      outputEl.addEventListener("input", (e) => {
        output = e.target.value;
        decode();
      });

      await tick();
      encode();
    }
  });
</script>

<svelte:head>
  <title>Toby's Base64 Encoder/Decoder</title>
  <meta property="og:description" content="Encode and Decode Base64. Fast and Free.">

</svelte:head>

<h1>Toby's Base64 Encoder/Decoder</h1>

<hr class="dashed" style="padding: 0%;"/>

<form class="form">
  <div class="container col">
    <div class="block">
      <label for="input">Input</label>
      <textarea id="input" bind:value={input} />
    </div>

    <div class="block">
      <label for="output">Output</label>
      <textarea id="output" readonly bind:value={output} />
    </div>
  </div>

  <div class="container col buttons">
    <button type="button" on:click={encode}>Encode</button>
    <button type="button" on:click={decode}>Decode</button>
  </div>
</form>

<hr class="dashed" />

<h3><a href="/">Toby Nott</a> / <a href="/tools">Tools</a> / <a href="/tools/base64">Base64</a></h3>

<style>
  button {
    color: black;
    margin: 5px;
  }
  textarea {
    color: black;
    width: 100%;
    height: 50%;
    margin: 5px;
  }

  .form {
    display: flex;
    justify-content: center;
    margin: 0 auto;
    width: 100%;
  }

  .container {
    display: flex;
    
    justify-content: center;
  }

  .col {
    flex-direction: column;
  }

  .block {
    display: block;
    margin: 5px;
  }
  .buttons{
    margin: 20px;
  }
</style>
