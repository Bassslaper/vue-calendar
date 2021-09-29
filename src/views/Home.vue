<template>
  <section id="calendar-page">
    <Calendar></Calendar>
  </section>  
</template>

<script>
import Calendar from '@/components/Calendar.vue'
// import { mapGetters } from 'vuex'
export default {
  components: { Calendar },
  name: 'Home',
  data () {
    return {
    }
  },
  computed: {
  
  },
  methods: {

  },
  mounted() {

  }

}
</script>

<style lang='scss' scoped>
  #calendar-page {
    height: 100%;
    padding: 4rem;
  }
</style>
