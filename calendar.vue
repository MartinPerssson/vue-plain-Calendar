<template lang="html">
  <div class="calendar">
        <div class="calendar-header">
            <i class="fa fa-fw fa-chevron-left" @click="subtractMonth"></i>
            <h4 style="display: inline;">{{month}}&nbsp;{{year}}</h4>
            <i class="fa fa-fw fa-chevron-right" @click="addMonth"></i>
        </div>
        <div>
          <ul class="cal-ul">
          <li class="cal-li" v-for="day in days">{{day}}</li>
          </ul>
        </div>
        <ul class="cal-ul">
            <li class="cal-li" v-for="date in daysInMonth"
        		:class="{'current-day': date == initialDate && month == initialMonth && year == initialYear}">
                <span>{{date}}</span>
            </li>
        </ul>
    </div>
</template>

<script>
import moment from 'moment'
export default {
  data () {
    return {
      today: moment(),
      dateContext: moment(),
      days: ['Monday', 'Tuesday', 'Wednesday', 'Thurday', 'Friday', 'Saturday', 'Sunday']
    }
  },
  computed: {
    year: function () {
      var t = this
      return t.dateContext.format('Y')
    },
    month: function () {
      var t = this
      return t.dateContext.format('MMMM')
    },
    daysInMonth: function () {
      var t = this
      return t.dateContext.daysInMonth()
    },
    currentDate: function () {
      var t = this
      return t.dateContext.get('date')
    },
    firstDayOfMonth: function () {
      var t = this
      var firstDay = moment(t.dateContext).subtract((t.currentDate - 1), 'days')
      return firstDay.weekday()
    },
    initialDate: function () {
      var t = this
      return t.today.get('date')
    },
    initialMonth: function () {
      var t = this
      return t.today.format('MMMM')
    },
    initialYear: function () {
      var t = this
      return t.today.format('Y')
    }
  },
  methods: {
    addMonth: function () {
      var t = this
      t.dateContext = moment(t.dateContext).add(1, 'month')
    },
    subtractMonth: function () {
      var t = this
      t.dateContext = moment(t.dateContext).subtract(1, 'month')
    }
  }
}
</script>

<style lang="css">
.calendar-header{
  display: inline-block;
  width: 100%;
  text-align: center;
}
.calendar-bar{
  text-align: center;
  font-size: 22px;
  width: 80%;
  margin-left: 10%;
  border-bottom: 5px solid lightgrey;
  margin-bottom: 30px;
}
.current-day{
  font-weight: bolder;
  border: 5px solid #FF6F6F !important;
  border-radius: 50%;
  color: #FF4646!important;
}
.calendar{
  margin-top: 10px;
  position: absolute;
}
.cal-ul {
    list-style: none;
    padding: 0;
    margin: 0;
    width: 100%;
}

.cal-li {
    display: block;
    float: left;
    width:14%;
    padding: 5px;
    box-sizing:border-box;
    margin-right: -1px;
    margin-bottom: -1px;
    font-size: 18px;
}

.cal-ul {
    height: 40px;
}

.cal-ul .cal-li {
    text-align: center;
    text-transform: uppercase;
    line-height: 50px;
    border: none;
    color: #000;
    font-size: 16px;
}

 .cal-li {
    height: 70px;
}
 .cal-li:hover {
    background: #d3d3d3;
    border-radius: 50%;
    cursor: pointer;
}
@media (max-width: 960px) {

 }
@media (max-width: 767px) {

}
</style>