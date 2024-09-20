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
        <th>Status</th>
        <th>Service</th>
        <th>Number</th>
        <th>Protocol</th>
        <th class="table-cell-fit">Description</th>
      </tr>
    </thead>
    <tbody>
      {#each tableData as row}
        <tr>
          {#if correctPorts.includes(row.number)}
            <td><i class="fa-solid fa-circle-check text-green-400"></i></td>
          {:else}
            <td><i class="fa-solid fa-circle-xmark text-red-600"></i> </td>
          {/if}
          <td>{row.service}</td>
          <td>{row.number}</td>
          <td>{row.protocol}</td>
          <td class="table-cell-fit"
            ><p class="text-wrap">{row.description}</p></td
          >
        </tr>
      {/each}
    </tbody>
  </table>
</div>
