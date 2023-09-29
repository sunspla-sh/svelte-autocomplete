<script lang="ts">
  import { countries } from "./assets/countryData.js";
  import Country from "./lib/Country.svelte";

  let countriesList = countries;

  let searchInput; //use with bind:this to focus input
  let inputValue = "";
  let hiLiteIndex = null;

  let selectedCountries = [];

  let filteredCountries = [];
  const filterCountries = () => {
    let storageArr = [];
    if (inputValue) {
      countriesList.forEach((country) => {
        if (country.toLowerCase().startsWith(inputValue.toLowerCase())) {
          storageArr = [...storageArr, country];
        }
      });
    }
    filteredCountries = storageArr;
  };

  $: if (!inputValue) {
    filteredCountries = [];
    hiLiteIndex = null;
  }

  const clearInput = () => {
    inputValue = "";
    searchInput.focus();
  };

  const setInputValue = (countryName) => {
    selectedCountries = [...selectedCountries, countryName];
    filteredCountries = [];
    const selectedIndex = countriesList.findIndex(c => c === countryName);
    countriesList.splice(selectedIndex, 1);
    hiLiteIndex = null;
    clearInput()
  };

  const submitValue = () => {
    if (inputValue) {
      setTimeout(clearInput, 1000);
    }
  };

  const navigateList = (e) => {
    if (e.key === "ArrowDown" && hiLiteIndex <= filteredCountries.length - 1) {
      hiLiteIndex === null ? hiLiteIndex = 0 : hiLiteIndex += 1;
    } else if (e.key === 'ArrowUp' && hiLiteIndex !== null) {
      hiLiteIndex === 0 ? hiLiteIndex = filteredCountries.length - 1 : hiLiteIndex -= 1;
    } else if (e.key === 'Enter') {
      setInputValue(filteredCountries[hiLiteIndex]);
    } else {
      return;
    }
  };
</script>
<svelte:window on:keydown={navigateList} />
<main>
  <form
    autocomplete="off"
    on:submit|preventDefault={submitValue}
  >
    <div class="autocomplete">
      <input
        id="country-input"
        type="text"
        placeholder="Search Country Names"
        bind:this={searchInput}
        bind:value={inputValue}
        on:input={filterCountries}
      >
      <!-- FILTERED LIST OF COUNTRIES -->
      {#if filteredCountries.length > 0}
        <ul id="autocomplete-items-list">
          {#each filteredCountries as country, i}
            <Country itemLabel={country} itemBold={inputValue.length} highlighted={i === hiLiteIndex} on:click={() => setInputValue(country)} />
          {/each}
        </ul>
      {/if}
    </div>

    <input type="submit">

    
  </form>
  <div>
    {#each selectedCountries as s}
      <p>{s}</p>
    {/each}
  </div>
</main>

<style>
  main {
    position: relative;
  }

  div.autocomplete {
    position: relative;
    display: inline-block;
    width: 300px;
  }
  input {
    border: 1px solid transparent;
    background-color: #f1f1f1;
    padding: 10px;
    font-size: 16px;
    margin: 0;
  }
  input[type="text"] {
    background-color: #f1f1f1;
    width: 100%;
  }
  input[type="submit"] {
    background-color: dodgerblue;
    color: #fff;
  }
  #autocomplete-items-list {
    position: absolute;
    margin: 0;
    padding: 0;
    top: 100%;
    width: 297px;
    max-height: 300px;
    overflow-y: scroll;
    scrollbar-width: thin;
    border: 1px solid #ddd;
    background-color: #ddd;
  }

  #autocomplete-items-list::-webkit-scrollbar {
    width: 8px;
    background-color: white;
  }

  /* #autocomplete-items-list::-webkit-scrollbar-track {
    width: 8px;
    background-color: gray;
  }  */

  #autocomplete-items-list::-webkit-scrollbar-thumb {
    width: 6px;
    background-color: lightgrey;
    border-radius: 4px;
    border: 1px solid white;
  }
</style>