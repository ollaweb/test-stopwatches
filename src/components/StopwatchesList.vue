<script>
import StopwatchesItem from '@/components/StopwatchesItem.vue'
import AddStopwatch from '@/components/AddStopwatch.vue'
export default {
    components: {
        StopwatchesItem,
        AddStopwatch
    },
    data() {
        return {
            stopwatches: [
                {
                    id: 1,
                    time: 160,
                    isRunning: false
                },
                {
                    id: 2,
                    time: 1532,
                    isRunning: false
                },
                {
                    id: 3,
                    time: 5415,
                    isRunning: false
                },
                {
                    id: 4,
                    time: 4833,
                    isRunning: false
                },
            ]
        }
    },
    methods: {
        addStopwatch() {
            this.stopwatches.push({
            id: this.stopwatches.length + 1,
            time: 0,
            isRunning: false
            })
        }
    }
}
</script>

<template>
    <ul class="stopwatches-list">
        <li v-for="stopwatch in stopwatches" :key="stopwatch.id">
            <StopwatchesItem :stopwatch="stopwatch"/>
        </li>
        <li>
            <AddStopwatch @add-stopwatch="addStopwatch"/>
        </li>
    </ul>
</template>

<style lang="scss">
.stopwatches-list {
    display: grid;
    grid-template-columns: 1fr;
    column-gap: 50px;
    row-gap: 45px;
    @media (min-width: 768px) {
        grid-template-columns: repeat(2,1fr);
    }
    @media (min-width: 1024px) {
        grid-template-columns: repeat(3,1fr);
    }
}
</style>