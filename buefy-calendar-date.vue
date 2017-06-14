<template>
    <div class="tile is-ancestor">
        <div v-for="n in 7" class="tile card is-vertical is-parent" v-bind:class="dates[n + offset].class">
            <header>
                <p>{{dates[n + offset].date}}</p>
            </header>

            <div class="card-content">
                <ul>
                    <li v-for="event in events[dates[n + offset].key]">
                        <a v-bind:href="event.url" target="_blank">
                            <span class="icon"><i class="fa fa-calendar-check-o"></i> {{event.title}}</span>
                        </a>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["dates", "events", "offset"]
    }
</script>

<style>
    .disabled {
        background-color: lightgrey!important;
    }
</style>