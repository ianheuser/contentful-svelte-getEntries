<script>
  // import our column component so we can add one for each product
  import Column from "./Column.svelte";

  // import the contentful api/sdk library to make calls to contentful easier
  // https://contentful.github.io/contentful.js/contentful/9.1.18/
  import * as contentful from "contentful";

  // create empty array to hold products that we call back
  // It needs to be an array as the #each loop in svelte only works looping over "array like objects"
  let products = [];

  /* Using the contentful library (imported on line 5), and the createClient function, 
              we connect to our contentful space and save that connection instance into the variable 
              "client" */
  const client = contentful.createClient({
    space: "3q892y4ckspg",
    accessToken: "w_ghIFLSyjNtCW4BdthHMn8WH21jXSC54suwYdXvxxQ",
    environment: "master"
  });

  //Call the getEntries() function on our client connection
  // https://contentful.github.io/contentful.js/contentful/9.1.18/ContentfulClientAPI.html#.getEntries
  client
    .getEntries({
      content_type: "product"
    })
    // then() gets called after a succesful connection
    // we save the returned data into a variable named response
    .then(response => {
      // response.items is an array at the second level of the returned data, and is the array of products we are looking for
      // so we save it into the products array we created up top
      products = response.items;
    })
    // catch() works like then() but is called upon any error being thrown in the call to the back end
    // similarly we save that info into a variable named "error"
    .catch(error => {
      //log that arror into the console
      console.log(error);
    });
</script>


<!-- The template -->
<main class="columns">

    <!-- using sveltes each loop, we loop over the 'products' array from line 11 -->
    {#each products as product}
      <!-- An instance of the column compnonent is created for every product -->
      <!-- data for individual products gets sent through parameters of our custom tag -->
      <Column heading={product.fields.name} blurb={product.fields.extendedBlurb} />
    {/each}

</main>



<!-- -->
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
