<script>
  import { onMount, afterUpdate } from 'svelte';
  import { writable } from 'svelte/store';

  import { createClient } from '@supabase/supabase-js';

  export let env = import.meta.env;

  let table = 'items';

  export const supabase = createClient(
      env.VITE_SUPABASE_URL, 
      env.VITE_SUPABASE_KEY
  );

  let fetchItems = async () => {
    var {data, error} = {};
    var { data, error } = await supabase
      .from(table).select()
    console.log(`Fetched items - `, data)
    if ( !error ) { return data; } else { throw error; }
  };

  let items = writable([])

  let updateItems = async () => {
    let updatedItems = await fetchItems()
      .then(results => { console.log(`Updated items - `, results); items.set(results)});
  };

  const itemsSub = supabase
    .from(table)
    .on('*', async () => {
      try {
        updateItems()
      } 
      catch(error) {
        throw(error);
      }})
    .subscribe();
  
  onMount(() => {
    updateItems();
  });

</script>

{#each $items as item}
  <p>{JSON.stringify(item)}</p>
{/each}