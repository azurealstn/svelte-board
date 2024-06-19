<script>
  // Flowbite UI Components
  import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell, Modal } from 'flowbite-svelte';

  import Header from '../components/Header.svelte'
  import Pagination from '../components/Pagination.svelte';

  // API 통신
  import axios from 'axios'

  // 컴포넌트가 DOM에 추가될 때 실행되는 스벨트 내장 API
  import { onMount } from 'svelte'

  // 상태를 유지하기 위한 필요한 변수들 선언
  let dataModels = [];
  let loading = true;
  let currentPage = 1;
  let totalPages = 1;
  let searchTerm = '';
  let showModal = false;
  const limit = 10;

  // 실제 API 통신 담당
  const fetchDataModels = async (page = 1) => {
    loading = true;
    try {
      const response = await axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=${limit}&q=${searchTerm}`);
      dataModels = response.data;
      totalPages = Math.ceil(response.headers['x-total-count'] / limit);
    } catch (err) {
      alert('에러가 발생하였습니다. \n관리자에게 문의해주세요.');
    } finally {
      loading = false;
      showModal = false;
    }
  };

  // 페이징에서 현재 페이지가 변경되면 바뀐 페이지로 fetchDataModels를 다시 호출한다.
  const changePage = (page) => {
    currentPage = page;
    fetchDataModels(page);
  }

  // 모달 on
  const openModal = () => {
    showModal = true;
  };

  // 모달 off
  const closeModal = () => {
    showModal = false;
    searchTerm = '';
  }

  // 컴포넌트가 DOM에 추가될 때 DataModel 데이터들을 가져온다.
  // onMount는 보통 네트워크 통신할 때 사용하게 된다.
  onMount(() => {
    fetchDataModels();
  });
</script>

<!-- 컴포넌트 적용 -->
<Header />

<div class="m-20">
  <div class="flex items-center justify-between">
    <h1>DataModel</h1>
    <!-- 이벤트 리스너: on:click, onkeydown 등등 -->
    <!-- 함수나 변수 적용 문법: {} 중괄호 안에 적는다. -->
    <button 
      on:click={openModal} 
      class="px-4 py-2 text-white bg-blue-600 rounded hover:bg-blue-700">
        Open Search Modal
    </button>
  </div>

  <Table>
    <TableHead>
      <TableHeadCell>userId</TableHeadCell>
      <TableHeadCell>id</TableHeadCell>
      <TableHeadCell>title</TableHeadCell>
      <TableHeadCell>body</TableHeadCell>
    </TableHead>
    <TableBody tableBodyClass="divide-y">
      <!-- 반복문 -->
      {#each dataModels as dataModel}
        <TableBodyRow>
          <TableBodyCell>{dataModel.userId}</TableBodyCell>
          <TableBodyCell>{dataModel.id}</TableBodyCell>
          <TableBodyCell>{dataModel.title}</TableBodyCell>
          <TableBodyCell>{dataModel.body}</TableBodyCell>
        </TableBodyRow>
      {/each}
    </TableBody>
  </Table>

  <!-- Props 사용 -->
  <Pagination {currentPage} {totalPages} on:pageChange={e => changePage(e.detail)} />
</div>

<Modal bind:open={showModal} size="lg" backdrop="static">
  <div class="p-4">
    <h3 class="text-lg font-medium">Search</h3>
    <input 
      type="text" 
      bind:value={searchTerm} 
      class="w-full p-2 mt-2 border border-gray-300 rounded" 
      placeholder="Enter search term..." />
    <div class="flex justify-end mt-4">
      <button 
        on:click={closeModal} 
        class="px-4 py-2 mr-2 text-gray-700 bg-gray-200 rounded hover:bg-gray-300">
          Close
      </button>
      <button 
        on:click={fetchDataModels}
        class="px-4 py-2 text-white bg-blue-600 rounded hover:bg-blue-700">
          Search
      </button>
    </div>
  </div>
</Modal>