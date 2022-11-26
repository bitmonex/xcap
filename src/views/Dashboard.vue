<template>
  <div>
      <Cmd />
    <h1>Dashboard</h1>
  </div>
</template>

<script>
    import Filters from '@/components/Filters'
    import Cmd from '@/components/Cmd'
    export default {
        name: 'Screener',
        components: {Cmd,Filters}
    }
</script>
