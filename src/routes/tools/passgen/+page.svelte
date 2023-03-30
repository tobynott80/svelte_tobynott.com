<script>
  import { onMount } from "svelte";
  import { tick } from "svelte";
  import { browser } from "$app/environment";

  let length = 8;
  let symbolsCheck = true;
  let numbersCheck = true;
  let uppercaseCheck = true;

  let password = "";

  const generatePassword = () => {
    const numbers = "0123456789";
    const lowerCaseLetters = "abcdefghijklmnopqrstuvwxyz";
    const upperCaseLetters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    const symbols = "!@#$%^&*()_+~`|}{[]:;?><,./-=";
    let characters = "";
    characters += lowerCaseLetters;
    if (symbolsCheck) {
      characters += symbols;
    }
    if (numbersCheck) {
      characters += numbers;
    }
    if (uppercaseCheck) {
      characters += upperCaseLetters;
    }
    let passwordValue = "";
    for (let i = 0; i < length; i++) {
      passwordValue += characters.charAt(
        Math.floor(Math.random() * characters.length)
      );
    }
    password = passwordValue;
  };

  const copyPassword = () => {
    let pw = document.querySelector("#password");
    pw.select();
    pw.setSelectionRange(0, 99999); /*For mobile devices*/
    document.execCommand("copy");
  };

  onMount(async () => {
    if (browser) {
      const lengthEl = document.getElementById("length");
      const symbolsEl = document.getElementById("symbols");
      const numbersEl = document.getElementById("numbers");
      const uppercaseEl = document.getElementById("uppercase");
      lengthEl.addEventListener("input", (e) => {
        length = e.target.value;
        generatePassword();
      });
      symbolsEl.addEventListener("input", (e) => {
        symbolsCheck = e.target.checked;
        generatePassword();
      });
      numbersEl.addEventListener("input", (e) => {
        numbersCheck = e.target.checked;
        generatePassword();
      });
      uppercaseEl.addEventListener("input", (e) => {
        uppercaseCheck = e.target.checked;
        generatePassword();
      });
      await tick();
      generatePassword();
    }
  });
</script>

<svelte:head>
  <title>Toby's Password Generator</title>
  <meta property="og:description" content="Create a secure password using Toby's Password Generator. Prevent security risks by using a strong, unique password">
</svelte:head>

<h1>Toby's Password Generator</h1>

<p>All passwords are randomised and generated client-side</p>

<hr class="dashed" />

<input type="text" id="password" readonly bind:value={password} />

<form class="form">
  <div class="container col">
    <label for="length">Length: {length}</label>
    <input type="range" min="4" max="16" bind:value={length} id="length" />
  </div>

  <div class="container col">
    <div class="block">
      <input type="checkbox" id="symbols" bind:checked={symbolsCheck} />
      <label for="symbols">Symbols</label>
    </div>
    <div class="block">
      <input type="checkbox" id="numbers" bind:checked={numbersCheck} />
      <label for="numbers">Numbers</label>
    </div>
    <div class="block">
      <input type="checkbox" id="uppercase" bind:checked={uppercaseCheck} />
      <label for="uppercase">Uppercase</label>
    </div>
  </div>
</form>

<div class="block">
  <button type="button" id="genPassword" on:click={generatePassword}
    >Generate Password</button
  >
  <button type="button" id="copyPassword" on:click={copyPassword}
    >Copy Password</button
  >
</div>

<hr class="dashed" />

<h3><a href="/">Toby Nott</a> / <a href="/tools">Tools</a> / <a href="/tools/passgen">Password Generator</a></h3>


<style>
  .form {
    display: flex;
    justify-content: center;
    margin: 0 auto;
    width: 100%;
  }

  .container {
    display: flex;
    margin: 15px;
    justify-content: center;
  }

  .col {
    flex-direction: column;
  }
  
  .block {
    display: block;
  }

  button {
    color: black;
  }

  #password {
    color: black;
  }

  label {
    display: inline-block;
    width: 0px;
    text-align: right;
  }
  h1, h3{
    margin: 10px;
  }
</style>
