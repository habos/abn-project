<script setup lang="ts">
  import useRecipes from '@/composibles/recipes';
  import { toRefs } from 'vue';

  const props = defineProps<{
    liveSearch: boolean;
  }>();

  //Property to determine whether input will be processed on input event or not
  const { liveSearch } = toRefs(props);
  let searchInput: string = '';

  function search() {
    useRecipes().getSearchedRecipes(searchInput);
  }
</script>

<template>
  <div class="searchBar">
    <input
      id="searchQueryInput"
      type="text"
      name="searchQueryInput"
      v-model="searchInput"
      v-on="liveSearch ? { input: search } : {}"
      @keypress.enter="search"
    />
    <button
      id="searchQuerySubmit"
      type="submit"
      name="searchQuerySubmit"
      @click="search"
    >
      <svg style="width: 20px; height: 20px" viewBox="0 0 24 24">
        <path
          fill="#666666"
          d="M9.5,3A6.5,6.5 0 0,1 16,9.5C16,11.11 15.41,12.59 14.44,13.73L14.71,14H15.5L20.5,19L19,20.5L14,15.5V14.71L13.73,14.44C12.59,15.41 11.11,16 9.5,16A6.5,6.5 0 0,1 3,9.5A6.5,6.5 0 0,1 9.5,3M9.5,5C7,5 5,7 5,9.5C5,12 7,14 9.5,14C12,14 14,12 14,9.5C14,7 12,5 9.5,5Z"
        />
      </svg>
    </button>
  </div>
</template>

<style scoped>
  .searchBar {
    display: flex;
    flex-direction: row;
    align-items: center;
  }

  #searchQueryInput {
    width: 16rem;
    height: 2rem;
    outline: none;
    border: none;
    border-radius: 1.625rem;
    padding: 0 3.5rem 0 1.5rem;
    font-size: 1rem;
  }

  #searchQuerySubmit {
    width: 3.5rem;
    height: 2.8rem;
    margin-left: -3.5rem;
    background: none;
    border: none;
    outline: none;
  }

  #searchQuerySubmit:hover {
    cursor: pointer;
  }

  svg {
    margin-top: 3px;
  }
</style>
