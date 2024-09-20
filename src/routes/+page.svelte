<script>
  import data from "$lib/data.json";
  import Practice from "../components/Practice.svelte";
  import Reset from "../components/Reset.svelte";
  import Table from "../components/Table.svelte";
  import { TabGroup, Tab, TabAnchor } from "@skeletonlabs/skeleton";
  let tabSet = 0;
</script>

<div class="container mx-auto">
  <TabGroup>
    <Tab bind:group={tabSet} name="tab1" value={0}>
      <!-- <svelte:fragment slot="lead">(icon)</svelte:fragment> -->
      <span>Study</span>
    </Tab>
    <Tab bind:group={tabSet} name="tab2" value={1}>Practice</Tab>
    <svelte:fragment slot="panel">
      {#if tabSet === 0}
        <div class="p-2">
          <div class="flex flex-row justify-between mb-2">
            <h2 class="h2">Ports</h2>
            <Reset />
          </div>

          <Table tableData={data} />
        </div>
      {:else if tabSet === 1}
        <div>
          <Practice ports={data} />
        </div>
      {:else if tabSet === 2}
        (tab panel 3 contents)
      {/if}
    </svelte:fragment>
  </TabGroup>
</div>
