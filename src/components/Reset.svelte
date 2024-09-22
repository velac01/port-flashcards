<script>
  // Function to clear correctPorts from localStorage
  function clearCorrectPorts() {
    if (typeof window !== "undefined") {
      localStorage.removeItem("correctPorts");
      alert("Progress Reset Successfully");
      window.location.reload()
    }
  }
</script>

<!-- Button to clear correctPorts from localStorage -->
<button
  on:click={clearCorrectPorts}
  class="btn p-2 bg-red-500 text-white rounded"
>
  Reset Progess
</button>
