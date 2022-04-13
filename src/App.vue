<template>
  <div id="app">
    <input type="number" v-model="limit" />
    <NumberSelector/>
  </div>
</template>

<script>
//Remnamed component to a multiword name in order to prevent conflicts with HTML elements.
import NumberSelector from '@/components/NumberSelector';

export default {
  name: 'App',
  //Added new component name
  components: {NumberSelector},
  data()
  {
    return {
      limit: 100,
    }
  }
}
</script>
//removed style tag as it is not necessary in this instance