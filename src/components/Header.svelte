<script>
  import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte';
  let activeUrl = window.location.pathname;
  if (activeUrl.includes('DataModel')) {
    activeUrl = '/DataModel';
  }
</script>

<Navbar>
  <NavBrand href="/">
    <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">
      City Data Hub
    </span>
  </NavBrand>
  <NavHamburger  />
  <NavUl {activeUrl} >
    <NavLi href="/DataModel">데이터 모델 관리</NavLi>
    <NavLi href="/DataSet">데이터 셋 관리</NavLi>
    <NavLi href="/AccessControl">데이터 접근 제어 관리</NavLi>
    <NavLi href="/ProvisionServer">Provision 서버 관리</NavLi>
    <NavLi href="/ExternalPlatform">외부 플랫폼 인증 관리</NavLi>
    <NavLi href="/VerificationHistory">품질 모니터링</NavLi>
    <NavLi href="/SystemManage">시스템 관리</NavLi>
  </NavUl>
</Navbar>