<script>
  import { createQrPngDataUrl } from '@svelte-put/qr';
  import { onMount } from 'svelte';

  let url = 'tobynott.com';
  let src = '';

  onMount(async () => { 
    if (typeof window !== 'undefined') {
      src = await createQrPngDataUrl({ 
        data: url,
        width: 500,
        height: 500,
        backgroundFill: '#fff',
      });
    }
  });

  $: if (typeof window !== 'undefined' && url) {
    (async () => {
      src = await createQrPngDataUrl({
        data: url,
        width: 500,
        height: 500,
        backgroundFill: '#fff',
      });
    })();
  }

</script>

<h1>QR Code Generator</h1>
<hr class="dashed" />
<div class="flex col">
  <label for="urlInput">Enter URL:</label>
  <input id="urlInput" type="text" bind:value={url} placeholder="Enter URL" />
  {#if src} 
    <img {src} width="180" height="180" alt="a qr code" />
    <a class="c-btn" href={src} download="qr {url}.png">Download QR as PNG</a>
  {/if}
</div>
<hr class="dashed" />
<h3 class="tx-sm mb-2">Created with <a href="https://github.com/vnphanquang/svelte-put/tree/main/packages/qr">@svelte-put/qr</a></h3>
<h3>
  <a href="/">Toby Nott</a> / <a href="/tools">Tools</a> /
  <a href="/tools/qrgen">QR Code Generator</a>
</h3>

<style>
  .tx-sm{
    font-size: 0.8rem;
  }
  .mb-2{
    margin-bottom: 0.4rem;
  }
  .flex{
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .col{
    flex-direction: column;
  }

  input{
    margin: 5px;
    color: black;
    width: auto;
  }
</style>