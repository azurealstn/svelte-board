<script>
  import { Route } from 'tinro'

  import AccessControl from './pages/AccessControl.svelte';
  import DataModel from './pages/DataModel.svelte';
  import DataModelRegist from './pages/DataModelRegist.svelte';
  import DataSet from './pages/DataSet.svelte';
  import ExternalPlatform from './pages/ExternalPlatform.svelte';
  import ProvisionServer from './pages/ProvisionServer.svelte';
  import SystemManage from './pages/SystemManage.svelte';
  import VerificationHistory from './pages/VerificationHistory.svelte'
</script>

<Route path='/' redirect='/DataModel' />
<Route path='/AccessControl'><AccessControl /></Route>
<Route path='/DataModel'><DataModel /></Route>
<Route path='/DataModelRegist'><DataModelRegist /></Route>
<Route path='/DataSet'><DataSet /></Route>
<Route path='/ExternalPlatform'><ExternalPlatform /></Route>
<Route path='/ProvisionServer'><ProvisionServer /></Route>
<Route path='/SystemManage'><SystemManage /></Route>
<Route path='/VerificationHistory'><VerificationHistory /></Route>