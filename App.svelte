<script>
  import Column from "./Column.svelte";
  import * as contentful from "contentful";
  let products = [];

  const client = contentful.createClient({
    space: "3q892y4ckspg",
    accessToken: "w_ghIFLSyjNtCW4BdthHMn8WH21jXSC54suwYdXvxxQ",
    environment: "master"
  });

  client
    .getEntries({
      content_type: "product"
    })
    .then(response => {
      products = response.items;
    })
    .catch(error => {
      console.log(error);
    });
</script>


<main class="columns">

    {#each products as product}
      <Column 
        heading={product.fields.name} 
        blurb={product.fields.extendedBlurb}
        calories={product.fields.calories} 
        fat={product.fields.fat}
        alcoholPercent={product.fields.alcoholPercent}
        carbs={product.fields.carbs}
      />
    {/each}

</main>


<style>
  .columns {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    margin: auto;
    width: 90%;
  }

  @media (max-width: 768px) {
    .columns {
      flex-direction: column;
    }
  }
</style>
