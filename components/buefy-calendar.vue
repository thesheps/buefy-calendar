<template>
    <div class="container">
        <div class="columns">
            <div class="column has-text-left"><a v-on:click="previous()"><i class="fa fa-chevron-left"></i></a></div>
            <div class="column has-text-centered"><h2 class="title is-2">{{currentMonth.format("MMMM YYYY")}}</h2></div>
            <div class="column has-text-right"><a v-on:click="next()"><i class="fa fa-chevron-right"></i></a></div>
        </div>
        <div class="tile is-ancestor">
            <div v-for="weekday in weekdays" class="tile card is-vertical is-hidden-mobile">
                <header class="card-header">
                    <p class="card-header-title">
                        {{weekday}}
                    </p>
                </header>
            </div>
        </div>

        <calendar-date :dates="dates" :events="events" :offset="0"></calendar-date>
        <calendar-date :dates="dates" :events="events" :offset="7"></calendar-date>
        <calendar-date :dates="dates" :events="events" :offset="14"></calendar-date>
        <calendar-date :dates="dates" :events="events" :offset="21"></calendar-date>
        <calendar-date :dates="dates" :events="events" :offset="28"></calendar-date>
    </div>
</template>

<script>
    import moment from 'moment';
    import CalendarDate from "./buefy-calendar-date.vue"

    const now = new moment(new Date().setDate(1));

    function getEmptyDate() {
        return { date: null, class: "is-hidden-mobile disabled" };
    }

    function getDates(start) {
        const days = Array.apply(null, { length: moment().daysInMonth() })
            .map(Number.call, Number)
            .map(function (i) {
                const d = start.clone().add(i, "days");
                return { date: d.format("Do"), key: d.format("YYYY-MM-DD") };
            });

        var dates = new Array(start.day()).fill(getEmptyDate()).concat(days);
        var length = dates.length;
        dates.length = 36;
        dates.fill(getEmptyDate(), length);

        return dates;
    }

    export default {
        props: ["events"],
        data() {
            return {
                showDates: true,
                currentMonth: now,
                dates: getDates(now),
                weekdays: [
                    "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"
                ]
            }
        },
        methods: {
            previous: function (offset) {
                this.currentMonth.subtract(1, "months");
                this.dates = getDates(this.currentMonth);
            },
            next: function (offset) {
                this.currentMonth.add(1, "months");
                this.dates = getDates(this.currentMonth);
            }
        },
        components: {
            'calendar-date': CalendarDate
        }
    }
</script>