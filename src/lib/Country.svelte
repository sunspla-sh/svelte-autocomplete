<script>
  /** @type string */
  export let itemLabel;
  export let itemBold;
  export let highlighted;
</script>

<li class="autocomplete-items" class:autocomplete-active={highlighted}>
  <button on:click class="autocomplete-button">
    <b>{itemLabel.substring(0, itemBold)}</b>{itemLabel.substring(itemBold)}
  </button>
</li>

<style>
  .autocomplete-items {
    list-style: none;
    border-bottom: 1px solid #d4d4d4;
    z-index: 99;
    top: 100%;
    left: 0;
    right: 0;
    cursor: pointer;
    background-color: #fff;
  }

  .autocomplete-button {
    border: 0;
    background: none;
    padding: 10px;
    width: 100%;
  }

  .autocomplete-items .autocomplete-button:hover {
    background-color: #81921f;
    color: white;
  }

  .autocomplete-items .autocomplete-button:active,
  .autocomplete-items .autocomplete-button:focus {
    /** when clicking */
    background-color: dodgerblue;
    color: #fff;
  }

  .autocomplete-active {
    /** when navigating with arrows */
    background-color: dodgerblue;
    color: #fff;
  }

</style>
