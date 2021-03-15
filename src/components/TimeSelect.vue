<template>
    <div class="timeSelect">
        <div class="timeSelect-header">Время</div>
        <div class="timeSelect-list">
            <div class="time" v-for="(time, index) in times" :key="index">{{time}}</div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Input",
    data() {
        return {
            times: ["10:00", "12:00", "14:00", "16:00", "18:00", "20:00", "22:00"]
        }
    }
}
</script>

<style scoped>
    .timeSelect {
        width: 92px;
        height: 182px;
        background: #FFFFFF;
        user-select: none;
    }
    .timeSelect-header {
        height: 24px;
        background: #E5E5E5;
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
        color: #333333;
    }
    .timeSelect-list {
        padding: 2px 4px;
        box-sizing: border-box;
    }
    .time {
        width: 84px;
        height: 20px;
        background: #F2F2F2;
        margin-bottom: 2px;
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
        color: #404040;
        cursor: pointer;
    }
</style>