<script>
export default {
    props: {
        stopwatch: {
            type: Object,
            required: true
        }
    },
    data() {
        return {
            runInterval: null
        }
    },
    computed: {
        seconds() {
            const numberOfSeconds = this.stopwatch.time;
            return numberOfSeconds > 60 ? numberOfSeconds % 60 : numberOfSeconds;
        },
        minutes() {
            const countedMinutes = Math.floor(this.stopwatch.time / 60);
            return countedMinutes > 60 ? countedMinutes % 60 : countedMinutes;
        },
        hours() {
            return Math.floor(this.stopwatch.time / 3600);
        }
    },
    methods: {
        start() {
            this.runInterval = setInterval(()=>{
                this.stopwatch.time ++;
            },1000)
            this.stopwatch.isRunning = true;
        },
        pause() {
            clearInterval(this.runInterval);
            this.stopwatch.isRunning = false
        },
        reset() {
            clearInterval(this.runInterval);
            this.stopwatch.time = 0;
            this.stopwatch.isRunning = false
        }
    }
}

</script>

<template>
    <div class="stopwatch">
        <div class="stopwatch__time" :class="{ active: stopwatch.isRunning }">
                <span class="stopwatch__hours" v-if="hours>0">{{ hours }}:</span>
            <span class="stopwatch__minutes" v-if="minutes >0"><span v-if="minutes < 10 && hours">0</span>{{ minutes }}:</span>
            <span class="stopwatch__seconds"><span v-if="seconds < 10 && minutes">0</span>{{ seconds }}</span>
        </div>
        <div class="stopwatch__controls">
            <div @click="pause" class="stopwatch__control" v-if="stopwatch.isRunning">
                <svg width="10" height="20" viewBox="0 0 10 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="7" width="3" height="20" fill="white"/>
                    <rect width="3" height="20" fill="white"/>
                </svg>
            </div>
            <div @click="start" class="stopwatch__control" v-else>
                <svg width="17" height="20" viewBox="0 0 17 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M0 20V0L17 10L0 20Z" fill="#9E9E9E"/>
                </svg>
            </div>
            <div @click="reset" class="stopwatch__control" :class="{ active: stopwatch.isRunning }">
                <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect width="20" height="20" fill="#9E9E9E"/>
                </svg>

            </div>
        </div>
    </div>
</template>

<style lang="scss">
.stopwatch {
    width: 225px;
    height: 120px;
    background-color: #696969;
    &__time {
        padding: 19px 0 20px;
        text-align: center;
        border-bottom: 1px solid #9E9E9E;
        &.active {
        color: #ffffff;
        border-bottom: 1px solid #ffffff;
    }
    }
    &__controls {
        padding: 20px 70px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        &:hover {
            cursor: pointer;
        }
    }
    &__control {
        &.active {
            & svg {
                & rect {
                    fill: #FFFFFF;
                }
            }
        }
    }
}
</style>