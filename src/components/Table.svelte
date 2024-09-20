<script>
  export let tableData;
  let correctPorts = [];
  if (typeof window !== "undefined") {
    correctPorts = JSON.parse(localStorage.getItem("correctPorts")) || [];
  }
</script>

<div class="table-container">
  <table class="table tabel-compact">
    <thead>
      <tr>
        <th class="table-cell-fit">Status</th>
        <th class="table-cell-fit">Service</th>
        <th class="table-cell-fit">Number</th>
        <th class="table-cell-fit">Protocol</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      {#each tableData as row}
        <tr>
          {#if correctPorts.includes(row.number)}
            <td class="flex justify-center"
              ><i class="fa-solid fa-circle-check text-green-400"></i></td
            >
          {:else}
            <td class="flex justify-center"
              ><i class="fa-solid fa-circle-xmark text-red-600"></i>
            </td>
          {/if}
          <td class="font-medium text-center">{row.service}</td>
          <td class="font-medium text-center">{row.number}</td>
          <td class="font-medium text-center">{row.protocol}</td>
          <td><p class="text-wrap">{row.description}</p></td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>
