<script>
  import { fade, fly } from "svelte/transition";
  export let heading;
  export let blurb;
  export let fat;
  export let calories;
  export let carbs;
  export let alcoholPercent;
</script>

<!-- A simple div with a heading and paragraph to be suppied by parent pages -->
<div class="column" transition:fly={{ y: 30, duration: 1000 }}>
		<h2>{ heading }</h2>
    <div class="info">
      <p>{ blurb }</p>
      <div class="nutritionInfo">
        <h5>Calories</h5>
        <p>{calories}</p>
      </div>
      <div class="nutritionInfo">
        <h5>Fat</h5>
        <p>{fat}</p>
      </div>
      <div class="nutritionInfo">
        <h5>Alcohol %</h5>
        <p>{alcoholPercent}</p>
      </div>
      <div class="nutritionInfo">
        <h5>Carbs</h5>
        <p>{carbs}</p>
      </div>
    </div>
		<button>Click Me</button>
</div>

<!-- styling of the div and its content -->
<style>
  .nutritionInfo {
    display: inline-block;
    width: 40%;
  }
  h2 {
    color: #12284c;
    font-family: "BudBold", "Helvetica Neue", Helvetica, Arial, sans-serif;
    font-size: 28px;
    text-align: center;
    text-transform: uppercase;
    font-weight: 900;
    height: 200px;
  }
  .column {
    flex: 1;
    display: flex;
    flex-direction: column;
    margin: 10px;
    border: 1px solid lightgrey;
    border-radius: 4px;
    padding: 0px 20px 20px;
    min-width: 250px;
    box-sizing: border-box;
    box-shadow: 7px 3px 10px rgba(0, 0, 0, 0.1);
  }

  .info {
    flex: 1;
  }

  button {
    padding: 15px;
  }

  @media (max-width: 768px) {
    .column {
      width: 100%;
      margin: 10px;
      padding: 0px 20px 20px;
    }
  }
</style>
