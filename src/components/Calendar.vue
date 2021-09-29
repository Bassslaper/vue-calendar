<template>
 <div class="calendar">
  <div class="calendar__select">
    <span class="arrow arrow_prev"></span>
    <span class="month">Март</span>
    <span class="arrow arrow_next"></span>
  </div>
  <div class="calendar__wrapper">
    <div class="calendar__header">
      <div
        class="calendar__header-item" 
        v-for="day in dayOfWeek"
        :key="day"
      >
        {{day}}
      </div>
    </div>
    <div class="calendar__table table">
      <div 
        v-for="(day, index) in days"
        :key="index"
        class="table__cell"
        :class="{today: isToday(day)}"
        :style="{ gridColumn: setColumn(index) }"
      >
        <span class="day">{{ day.format('D') }}</span>
      </div>
    </div>
  </div>
 </div>
</template>

<script>
import * as momentTemp from 'moment';
const moment = momentTemp["default"];

export default {
  name: 'Calendar',
  components: {  },
  data () {
    return {
      dayOfWeek: ['Понедельник', 'Вторник','Среда','Четверг','Пятница','Суббота','Воскресенье'],
      days: []
    }
  },
  computed: {
  },
  methods: {
    setColumn(index) {
      if (index == 0) {
        return this.days[0].day() + 1
      }
    },
    isToday (day) {
      return moment().isSame(day, 'day')
    }
  },

  mounted () {
    let monthDate = moment().startOf('month')

    this.days = [...Array(monthDate.daysInMonth())].map((_, index) => {
      return monthDate.clone().add(index, 'day')
    })
    console.log('this.days: ', this.days);
  }
}
</script>

<style lang="scss" scoped>
  .calendar {
    display: flex;
    flex-direction: column;
    width: fit-content;
    height: fit-content;
    margin: 0 auto;
    padding: 3rem;
    border-radius: 2rem;
    background: #FFFFFF;
    box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.25);

    &__select {
      flex-grow: 0;
      margin-bottom: 2.5rem;
      display: flex;
      align-items: center;

      .arrow {
        display: block;
        width: 2rem;
        height: 2rem;
        background-position: center center;
        background-size: contain;
        background-repeat: no-repeat;

        &_prev {
          background-image: url('../assets/img/icons/left-arrow.svg');
        }

        &_next {
          background-image: url('../assets/img/icons/next.svg');
        }
      }
      .month {
        margin-right: 1rem;
        margin-left: 1rem;
        text-transform: uppercase;
        font-weight: 600;
        color: $month-color;
      }
    }

    &__wrapper {
      flex-grow: 1;
      display: flex;
      flex-direction: column;
    }

    &__header {
      padding: 0 0.5rem;
      flex-grow: 0;
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      grid-template-rows: 1fr;
      grid-column-gap: 0.5rem;

      &-item {
        padding-top: 0.5rem;
        padding-bottom: 1rem;
        font-weight: 600;
        text-align: right;
        text-transform: uppercase;
      }
    }

    &__table {
      flex-grow: 1;
    }
    
    .table {
      background-color: $bg-color;
      padding: 0.5rem;
      height: 100%;
      border-radius: 2rem;
      display: grid;
      grid-template-rows: repeat(5, 16.4rem);
      grid-template-columns: repeat(7, 16.4rem);
      grid-auto-rows: 16.4rem;
      grid-gap: 0.5rem;

      &__cell {
        background-color: #fff;
        box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.15);
        border-radius: 2rem;
        position: relative;

        .day {
          position: absolute;
          top: 2rem;
          right: 1rem;
        }

        &.today {
          .day {
            color: $today-color;
            font-weight: 600;
          }
        }
      }
    }
  }
</style>
