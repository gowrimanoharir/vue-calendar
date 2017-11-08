<template>
<div>
  <!-- <vue-datepicker-local v-model="timeRange" format="YYYY-MM-DD HH:mm:ss" :disabled-date="disabledDate"/><br/>
  <vue-datepicker-local v-model="timeRange" format="YYYY-MM-DD HH:mm:ss" :disabled-date="disabledDate" :local="local" range-separator="至"/><br/> -->
  <vue-datepicker-local v-model="time" format="DD-MMM-YYYY" :local="local" v-on:date-change="dateChange"/><br/>
  <!-- <vue-datepicker-local v-model="time" format="YYYY-MM"/><br/>
  <vue-datepicker-local v-model="time" format="YYYY"/><br/>
  <vue-datepicker-local v-model="empty" format="YYYY-MM-DD HH:mm:ss" clearable placeholder="select date"/><br/>
  <vue-datepicker-local v-model="now" disabled/> -->
</div>
</template>

<script>
export default {
  name: 'App',
  data () {
    const min = new Date(2017, 5, 1, 0, 0, 0)
    const max = new Date(2017, 8, 30, 0, 0, 0)
    const now = new Date()
    return {
      empty: '',
      now: now,
      time: min,
      min: min,
      max: max,
      timeRange: [min, max],
      local: {
        dow: 4, // Sunday is the first day of the week
        hourTip: 'Select Hour', // tip of select hour
        minuteTip: 'Select Minute', // tip of select minute
        secondTip: 'Select Second', // tip of select second
        yearSuffix: '', // suffix of head
        monthsHead: 'January_February_March_April_May_June_July_August_September_October_November_December'.split('_'), // months of head
        months: 'Jan_Feb_Mar_Apr_May_Jun_Jul_Aug_Sep_Oct_Nov_Dec'.split('_'), // months of panel
        weeks: 'Su_Mo_Tu_We_Th_Fr_Sa'.split('_') // weeks
      }
    }
  },
  methods: {
    disabledDate (time) {
      return time < this.min || time > this.max
    },
    dateChange (date) {
      const re=/((0[1-9])|(1[0-2]))[\/-]((0[1-9])|(1[0-9])|(2[0-9])|(3[0-1]))[\/-](\d{4})/;
      if(re.test(date)){
      const i = date.split('/');
      const ndat = new Date(parseInt(i[2]), parseInt(i[0])-1, parseInt(i[1]), 0, 0, 0)
      console.log(re.test(date));
      this.time=ndat;
      }
      else{
        alert('invalid date format')
      }
    }
  }
}
</script>
