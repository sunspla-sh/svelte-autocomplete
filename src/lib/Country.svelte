<script>
  export let itemLabel;
  export let highlighted;
</script>

<li class="autocomplete-items" class:autocomplete-active={highlighted} on:click >{@html itemLabel}</li>

<style>
  .autocomplete-items {
    list-style: none;
    border-bottom: 1px solid #d4d4d4;
    z-index: 99;
    top: 100%;
    left: 0;
    right: 0;
    padding: 10px;
    cursor: pointer;
    background-color: #fff;
  }
  .autocomplete-items:hover{
    background-color: #81921f;
    color: white;
  }

  .autocomplete-items:active {
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