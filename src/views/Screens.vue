<template>
  <div>
    <Cmd />
    <h1>Screens</h1>
    <Filters />

  </div>
</template>

<script>
    import Cmd from '@/components/Cmd'
    import Filters from '@/components/Filters'
    export default {
        name: 'Screener',
        components: {Cmd,Filters}
    }
</script>
