<script>
  let DateInput = "";
  let EpochInput = "";
  let outputType = "seconds";
  let inputType = "seconds";
  let OutputEpochValue = "";
  let OutputDateValue = "";

  function convertDate() {
    const dateValue = new Date(DateInput);
    if (!isNaN(dateValue.getTime())) {
      if (outputType === "timestamp") {
        OutputEpochValue = dateValue.getTime().toString();
      } else {
        OutputEpochValue = Math.floor(dateValue.getTime() / 1000).toString();
      }
    } else {
      OutputEpochValue = "Invalid date input";
    }
  }
  function convertEpoch() {
    const epochValue = parseInt(EpochInput);
    if (inputType === "timestamp") {
      if (epochValue.toString().length === 13) {
        OutputDateValue = new Date(epochValue).toISOString();
      } else {
        OutputDateValue = "Invalid timestamp input";
      }
    } else {
      if (epochValue.toString().length === 10) {
        OutputDateValue = new Date(epochValue * 1000).toISOString();
      } else {
        OutputDateValue = "Invalid timestamp input";
      }
    }
  }
</script>

<h1>Unix Epoch Converter</h1>
<hr class="dashed" />
<h2><u>Date → Epoch</u></h2>
<h3>Convert a date time to a Unix timestamp</h3>

<div>
  <label>
    Date Input:
    <input
      type="datetime-local"
      bind:value={DateInput}
      on:input={convertDate}
    />
  </label>
</div>
<div>
  <label>
    Output Type:
    <select bind:value={outputType} on:change={convertDate}>
      <option value="timestamp">Timestamp (milliseconds)</option>
      <option value="seconds">Unix Timestamp (seconds)</option>
    </select>
  </label>
</div>
<div>
  <label>
    Output Value:
    <input type="text" readonly value={OutputEpochValue} />
  </label>
</div>

<h2><u>Epoch → Date</u></h2>
<h3>Convert a Unix timestamp to a date</h3>
<div>
  <label>
    Epoch Input:
    <input type="number" bind:value={EpochInput} on:input={convertEpoch} />
  </label>
</div>
<div>
  <label>
    Input Type:
    <select bind:value={inputType} on:change={convertEpoch}>
      <option value="timestamp">Timestamp (milliseconds)</option>
      <option value="seconds">Unix Timestamp (seconds)</option>
    </select>
  </label>
</div>
<div>
  <label>
    Output Date:
    <input type="text" readonly value={OutputDateValue} />
  </label>
</div>

<hr class="dashed" />

<h3>
  <a href="/">Toby Nott</a> / <a href="/tools">Tools</a> /
  <a href="/tools/epoch">Epoch Converter</a>
</h3>

<style>
  input,
  select,
  option {
    margin: 5px;
    color: black;
  }
  label {
    width: 0px;
    text-align: left;
  }
  h1 {
    margin: 10px;
  }
  h2 {
    font-size: 1em;
    padding: 0px;
  }
</style>
