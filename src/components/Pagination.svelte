<script>
  export let currentPage;
  export let totalPages;

  import { createEventDispatcher } from 'svelte';

  // 부모 컴포넌트의 기능을 자식 컴포넌트에서 사용하고 싶을 때
  const dispatch = createEventDispatcher();

  const handlePageChange = (page) => {
    dispatch('pageChange', page);
  };
</script>

<nav aria-label="Page navigation" class="mt-4">
  <ul class="inline-flex items-center -space-x-px">
    <li>
      <button 
        on:click={() => handlePageChange(1)} 
        class="px-3 py-2 ml-0 leading-tight text-gray-500 bg-white border border-gray-300 rounded-l-lg hover:bg-gray-100 hover:text-gray-700" 
        disabled={currentPage === 1}>
        First
      </button>
    </li>
    <li>
      <button 
        on:click={() => handlePageChange(currentPage - 1)} 
        class="px-3 py-2 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700" 
        disabled={currentPage === 1}>
        Previous
      </button>
    </li>
    {#each Array(totalPages).fill(0).map((_, i) => i + 1) as page}
      <li>
        <button 
          on:click={() => handlePageChange(page)}  
          class="px-3 py-2 leading-tight text-gray-500 border border-gray-300 hover:bg-gray-100 hover:text-gray-700 
          {page === currentPage ? 'bg-blue-50 text-blue-600' : 'bg-white'}">
          {page}
        </button>
      </li>
    {/each}
    <li>
      <button
        on:click={() => handlePageChange(currentPage + 1)} 
        class="px-3 py-2 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700" 
        disabled={currentPage === totalPages || totalPages === 0}>
        Next
      </button>
    </li>
    <li>
      <button 
        on:click={() => handlePageChange(totalPages)} 
        class="px-3 py-2 leading-tight text-gray-500 bg-white border border-gray-300 rounded-r-lg hover:bg-gray-100 hover:text-gray-700" 
        disabled={currentPage === totalPages || totalPages === 0}>
        Last
      </button>
    </li>
  </ul>
</nav>

<style>
  nav {
    display: flex;
    justify-content: center;
    margin-top: 20px;
  }
  button:disabled {
    cursor: not-allowed;
    opacity: 0.5;
  }
</style>