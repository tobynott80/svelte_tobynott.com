<script>
    import qrcode from 'qrcode';

    let url = "https://tobynott.com";

    const generate = () => {
        return qrcode.toDataURL(url)
    };
</script>

<form>
    <div class="container col">
        <label for="url">Url:</label>
        <input type="url" id="url" bind:value={url}/>
    </div>
    <input id="generate" type="submit" value="Generate QR Code" on:click={generate}/>
</form>

<style>
    input{
        color: black;
        width: 40%;
    }
    #generate{
        width: fit-content;
    }
</style>