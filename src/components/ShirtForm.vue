<template>
    <div class="shirtForm">
        <div class="preview-wrapper">
            <div class="preview"></div>
            <div class="color-picker">
                <div class="color" v-for="(color, index) in colors" :key="index" :style="{background: color}"></div>
            </div>
        </div>
        <div class="form-inputs">
            <div class="print-picker">
                <div class="print"></div>
                <div class="print"></div>
                <div class="print"></div>
                <div class="print"></div>
                <div class="print"></div>
                <div class="print"></div>
                <div class="print"></div>
            </div>
            <div class="custom-inputs">
                <Calendar />
                <TimeSelect />
                <div class="position-picker">
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                    <div class="position"></div>
                </div>
            </div>
            <div class="submit">Подтвердить</div>
        </div>
    </div>
</template>

<script>
import Calendar from './Calendar.vue'
import TimeSelect from './TimeSelect.vue'

export default {
    name: "ShirtForm",
    components: {
        Calendar,
        TimeSelect
    },
    data() {
        return {
            colors: []
        }
    },
    created() {
        this.colors = ["#000000", "#FFFFFF", "#FF0000", "#00FF00", "#0000FF"]
    }
}
</script>

<style scoped>
    .shirtForm {
        display: flex;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
        width: 1200px;
        height: 720px;
        background: #F7F7F7;
        border-radius: 5px;
        filter: drop-shadow(0px 4px 20px rgba(0, 0, 0, 0.15));
    }
    .preview-wrapper {
        position: relative;
        height: 100%;
        width: 576px;
        padding: 24px 48px;
        box-sizing: border-box;
    }
    .preview {
        height: 100%;
        width: 100%;
        background: #FFFFFF;
        border: 2px solid #EBEBEB;
        border-radius: 5px;
    }
    .color-picker {
        position: absolute;
        display: flex;
        flex-direction: column;
        height: 276px;
        width: 72px;
        bottom: 36px;
        right: 24px;
        background: #FFFFFF;
        box-shadow: 2px 4px 21px rgba(0, 0, 0, 0.15);
        border-radius: 5px;
        gap: 3px;
        padding: 12px;
        box-sizing: border-box;
    }
    .color {
        width: 48px;
        height: 48px;
        background: black;
        cursor: pointer;
    }
    .color:nth-child(2) {
        border: 1px solid #E5E5E5;
        box-sizing: border-box;
    }
    .form-inputs {
        flex: 1;
        padding: 36px 48px 48px 24px;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
    }
    .print-picker {
        display: flex;
        background: #FFFFFF;
        border: 2px solid #EBEBEB;
        padding: 24px;
        box-sizing: border-box;
        border-radius: 5px;
        gap: 6px;
        width: 556px;
        flex-wrap: wrap;
        margin: 0;
    }
    .print {
        width: 96px;
        height: 96px;
        background: #F2F2F2;
        border: 1px solid #CCCCCC;
        box-sizing: border-box;
        cursor: pointer;
    }
    .custom-inputs {
        display: flex;
        justify-content: space-between;
    }
    .position-picker {
        width: 180px;
        height: 180px;
        background: #FFFFFF;
        display: grid;
        grid-template-columns: repeat(3, 54px);
        grid-template-rows: repeat(3, 54px);
        gap: 4px;
        padding: 5px;
        box-sizing: border-box;
    }
    .position {
        background: #E5E5E5;
        cursor: pointer;
    }
    .submit {
        background: #333333;
        width: 288px;
        height: 72px;
        border-radius: 5px;
        font-family: Arial;
        font-style: normal;
        font-weight: normal;
        font-size: 24px;
        line-height: 28px;
        display: flex;
        align-items: center;
        justify-content: center;
        text-align: center;
        letter-spacing: 0.12em;
        text-transform: uppercase;
        color: #DADADA;
        margin: 0 auto;
        user-select: none;
        cursor: pointer;
}
</style>