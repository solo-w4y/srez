<template>
    <div class="calendar">
        <div class="year">
            <div class="year-text">{{month.year}}</div>
        </div>
        <div class="calendar-body">
            <div class="month-change">
                <div class="month-prev" @click="changeSelected(0)" v-bind:class="{active: selected}">
                    <svg width="6" height="11" viewBox="0 0 6 11" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M5.5 10L1 5.5L5.5 1" stroke="#333333" stroke-linecap="round"/>
                    </svg>
                </div>
                <div class="month">{{month.name}}</div>
                <div class="month-next" @click="changeSelected(1)" v-bind:class="{active: !selected}">
                    <svg width="7" height="11" viewBox="0 0 7 11" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M1 1L5.5 5.5L1 10" stroke="#333333" stroke-linecap="round"/>
                    </svg>
                </div>
            </div>
            <div class="week">
                <div class="week-day">Пн</div>
                <div class="week-day">Вт</div>
                <div class="week-day">Ср</div>
                <div class="week-day">Чт</div>
                <div class="week-day">Пт</div>
                <div class="week-day">Сб</div>
                <div class="week-day">Вс</div>
            </div>
            <div class="days">
                <div class="day" v-for="(day, index) in month.days" :key="index" v-bind:class="{available: day.a, holiday: day.h, today: day.t}">{{day.n}}</div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Calendar",
    data() {
        return {
            month: {},
            selected: 0
        }
    },
    computed: {},
    methods: {
        fillMonth: function(selected) {
            let today = new Date(),
                thisMonth = [];
            today.setMonth(today.getMonth() + selected)
            if(new Date(today.getFullYear(), today.getMonth(), 1).getDay() > 0) {
                for(let i = 0, h = false, dw = 0, d = new Date(today.getFullYear(), today.getMonth(), 0).getDate(); i < new Date(today.getFullYear(), today.getMonth(), 1).getDay()-1; i++, d--) {
                    dw = new Date(today.getFullYear(), today.getMonth(), i).getDay()
h = false
                    if(dw === 0 || dw === 6) {
                        h = true
                    }
                    thisMonth.unshift({
                        n: d,
                        a: false,
                        h: h,
                        t: false
                    })
                }
            } else if (new Date(today.getFullYear(), today.getMonth(), 1).getDay() === 0) {
                for(let i = 0, h = false, dw = 0, d = new Date(today.getFullYear(), today.getMonth(), 0).getDate(); i < 6; i++, d--) {
                    dw = new Date(today.getFullYear(), today.getMonth(), i).getDay()
                    h = false
                    if(dw === 0 || dw === 6) {
                        h = true
                    }
                    thisMonth.unshift({
                        n: d,
                        a: false,
                        h: h,
                        t: false
                    })
                }
            }
            for(let i = 1, a = true, dw = 0, h = false, t = false, prevday = true; i <= new Date(today.getFullYear(), today.getMonth() + 1, 0).getDate(); i++) {
                dw = new Date(today.getFullYear(), today.getMonth(), i).getDay()
                if(!this.selected) {
                    if(i > today.getDate()) {
                        prevday = false
                    }
                    if(i === today.getDate()) {
                        t = true
                    } else {
                        t = false
                    }
                } else {
                    prevday = false
                }
                h = false
                if(dw === 0 || dw === 6) {
                    a = false
                    h = true
                } else if(prevday) {
                    a = false
                } else {
                    a = true
                }
                thisMonth.push({
                    n: i,
                    a: a,
                    h: h,
                    t: t
                })
            }
            let thisMonthLength = 42 - thisMonth.length;
            for(let i = 1, h = false, dw = 0; i <= thisMonthLength; i++) {
                dw = new Date(today.getFullYear(), today.getMonth()+1, i).getDay()
                h = false
                if(dw === 0 || dw === 6) {
                    h = true
                }
                thisMonth.push({
                    n: i,
                    a: false,
                    h: h,
                    t: false
                })
            }
            return {
                year: today.getFullYear(),
                name: today.toLocaleDateString('ru-RU', {month: 'long'}),
                days: thisMonth
            }
        },
        changeSelected: function(selected) {
            this.selected = selected;
            this.month = this.fillMonth(this.selected)
            console.warn(this.month)
        }
    },
    created() {
        this.month = this.fillMonth(this.selected)
    }
}
</script>

<style scoped>
    .calendar {
        width: 184px;
        height: 182px;
        background: #FFFFFF;
        display: flex;
        user-select: none;
    }
    .year {
        width: 24px;
        height: 182px;
        background: #333333;
    }
    .year-text {
        width: 24px;
        height: 182px;
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        line-height: 14px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        letter-spacing: 0.3em;
        text-transform: capitalize;
        color: #F2F2F2;
        writing-mode: vertical-lr;
        transform: rotate(180deg);
    }
    .month-change {
        width: 160px;
        height: 24px;
        background: #E5E5E5;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding-left: 9px;
        padding-right: 9px;
        box-sizing: border-box;
    }
    .month-prev, .month-next {
        cursor: pointer;
    }
    .month-prev:is(.active):hover path, .month-next:is(.active):hover path {
        stroke-opacity: 0.7;
    }
    .month-prev:not(.active), .month-next:not(.active) {
        cursor: initial;
        opacity: 0.4;
    }
    .month {
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        line-height: 14px;
        display: flex;
        align-items: center;
        text-align: center;
        text-transform: capitalize;
        color: #333333;
    }
    .week {
        display: flex;
        gap: 2px;
        width: 160px;
        height: 20px;
        background: #333333;
        padding-left: 4px;
        padding-right: 4px;
        box-sizing: border-box;
    }
    .week-day {
        width: 20px;
        height: 20px;
        color: #F2F2F2;
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-transform: capitalize;
    }
    .days {
        display: grid;
        grid-template-columns: repeat(7, 20px);
        grid-template-rows: repeat(6, 20px);
        gap: 2px;
        padding: 4px;
    }
    .day {
        color: rgba(51, 51, 51, 0.75);
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 12px;
        line-height: 14px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        text-transform: capitalize;
        font-feature-settings: 'tnum' on, 'lnum' on;
        background: #F0F0F0;
        cursor: pointer;
    }
    .day:is(.available):hover {
        background: #CCCCCC;
        position: relative;
    }
    .day:not(.available) {
        color: rgba(51, 51, 51, 0.35);
        background: #FFFFFF;
        cursor: initial;
    }
    .day:is(.today) {
        border: 1px solid rgba(51, 51, 51, 0.2);
        box-sizing: border-box;
    }
    .day:is(.holiday) {
        background: #D9D9D9;
        color: rgba(51, 51, 51, 0.45);
    }
</style>