<script>
  import { ProgressBar } from "@skeletonlabs/skeleton";
  export let ports;
  let userPort = "";
  let userProtocol = "";
  let feedbackMessage = "";
  let showHint = false;
  function checkAnswer() {
    if (
      parseInt(userPort) === ports[index].number &&
      userProtocol.toUpperCase() === ports[index].protocol.toUpperCase()
    ) {
      feedbackMessage = "Correct! You matched both the port and the protocol.";
      let correctPorts = JSON.parse(localStorage.getItem("correctPorts")) || [];
      if (!correctPorts.includes(ports[index].number)) {
        correctPorts.push(ports[index].number);
        localStorage.setItem("correctPorts", JSON.stringify(correctPorts));
      }
    } else {
      feedbackMessage = "Incorrect. Try again.";
    }
  }

  let index = 0;
  function handleNav(isNext) {
    userPort = "";
    userProtocol = "";
    feedbackMessage = "";
    if (isNext) {
      index += 1;
    } else {
      index -= 1;
    }
  }
</script>

<div class="flex flex-col gap-2">
  <div class="p-2">
    <ProgressBar value={index + 1} max={ports.length} meter={"bg-blue-500"} />
  </div>

  <div class="card p-4 mx-2">
    <div class="container mx-auto flex flex-col gap-2">
      <div
        class="flex flex-row w-full"
        class:justify-between={index > 0}
        class:justify-end={index === 0}
      >
        <button
          class={index > 0 ? "" : "hidden"}
          on:click={() => handleNav(false)}>Back</button
        >
        <button
          class={index < ports.length - 1 ? "" : "hidden"}
          on:click={() => handleNav(true)}>Next</button
        >
      </div>
      <div class="flex flex-col">
        <h2 class="h2 text-center">{ports[index].service}</h2>
        <input
          type="number"
          placeholder="Enter Port Number"
          bind:value={userPort}
          class="input mt-4 p-2 border rounded"
        />
        <input
          type="text"
          placeholder="Enter Protocol (e.g., TCP/UDP)"
          bind:value={userProtocol}
          class="input mt-2 p-2 border rounded"
        />
        <!-- Button to submit answer -->
        <button
          on:click={checkAnswer}
          class="btn mt-4 p-2 bg-blue-500 text-white rounded"
        >
          Submit
        </button>
        <!-- Feedback Message -->
        {#if feedbackMessage}
          <p class="feedback mt-4">{feedbackMessage}</p>
        {/if}
        <div class="flex flex-row justify-end pt-2">
          <button
            on:click={() => (showHint = !showHint)}
            aria-roledescription="clc"
          >
            {#if showHint}
              Hide Hint
            {:else}
              Show Hint
            {/if}</button
          >
        </div>
        {#if showHint}
          <div class="flex flex-row gap-2">
            <p>{ports[index].service}</p>
            <p>{ports[index].number}</p>
            <p>{ports[index].protocol}</p>
          </div>
        {/if}
      </div>
    </div>
  </div>
</div>
