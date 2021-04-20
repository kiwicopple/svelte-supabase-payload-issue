<script>
  import { onMount, afterUpdate } from "svelte";
  import { writable } from "svelte/store";

  import { createClient } from "@supabase/supabase-js";

  export let env = import.meta.env;

  let table = "items";

  const supabase = createClient(env.VITE_SUPABASE_URL, env.VITE_SUPABASE_KEY);

  let fetchItems = async () => {
    var { data, error } = await supabase.from(table).select();
    if (error) {
      throw error;
    } else {
      return data;
    }
  };

  let items = writable([]);

  let updateItems = async () => {
    try {
      let updatedItems = await fetchItems();
      items.set(updatedItems);
    } catch (error) {
      console.error(error.message)
    }
  };

  const itemsSub = supabase
    .from(table)
    .on("*", (payload) => {
      console.log("payload", payload);
      updateItems()
    })
    .subscribe();

  onMount(() => {
    updateItems();
  });
</script>

{#each $items as item}
  <p>{JSON.stringify(item)}</p>
{/each}
