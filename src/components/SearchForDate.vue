<template>
    <van-popup class="searchForDate" v-model="show" closeable>
        <div>
            <van-row>
                <van-col span="8">
                    <van-button @click="selectDate('3')" :type="currentSelect == '3' ? 'primary' : 'default'">最近三天</van-button>
                </van-col>
                <van-col span="8">
                    <van-button @click="selectDate('7')" :type="currentSelect == '7' ? 'primary' : 'default'">最近七天</van-button>
                </van-col>
                <van-col span="8">
                    <van-button @click="selectDate('0')" :type="currentSelect == '0' ? 'primary' : 'default'">自定义</van-button>
                </van-col>
            </van-row>
            <div v-if="showSelectTime">
                <van-field :readonly="isReadOnly" name="startTime" :value="startTimeValue" label="开始时间"
                    placeholder="点击选择日期" @click="isReadOnly ? '' : showCalendar_startTime = true" />
                <van-field readonly clickable name="endTime" :value="endTimeValue" label="结束时间" placeholder="点击选择日期"
                    @click="isReadOnly ? '' : showCalendar_endTime = true" />
            </div>
            <van-calendar v-model="showCalendar_startTime" @confirm="onConfirmStartTime" get-container="#app" />
            <van-calendar v-model="showCalendar_endTime" @confirm="onConfirmEndTime" get-container="#app"
                :min-date="minEndTime" />

        </div>

        <div class="optionBtns">
            <van-button @click="onReset">重置</van-button>
            <van-button type="primary" @click="onFilter">确定</van-button>
        </div>
    </van-popup>
</template>
<script>
    // @ is an alias to /src
    import { Button, Col, Row, Popup, Field, Calendar } from 'vant';

    export default {
        name: 'SearchForDate',
        components: {
            [Button.name]: Button,
            [Col.name]: Col,
            [Row.name]: Row,
            [Popup.name]: Popup,
            [Field.name]: Field,
            [Calendar.name]: Calendar,
        },
        props: ["showSearch"],
        data() {
            return {
                show: false,
                startTimeValue: '',
                endTimeValue: '',
                showCalendar_startTime: false,
                showCalendar_endTime: false,
                isReadOnly: true,
                showSelectTime: false,
                currentSelect: ''
            }
        },
        methods: {
            onReset() {
                this.show = false;                
                this.currentSelect = "";
                this.showSelectTime = false;
                this.startTimeValue = "";
                this.endTimeValue = "";
                this.emitFilterData();
            },
            onFilter() {
                this.show = false;
                this.emitFilterData();
            },
            emitFilterData() {
                let _data = {
                    startTime: this.startTimeValue,
                    endTime: this.endTimeValue
                }
                this.$emit("filterData", _data)
            },
            showPopup() {
                this.show = true;
            },
            hidePopup() {
                this.show = false;
            },
            onConfirmStartTime(date) {
                this.startTimeValue = this.timeFormate(date);
                this.showCalendar_startTime = false;
            },
            onConfirmEndTime(date) {
                this.endTimeValue = this.timeFormate(date);
                this.showCalendar_endTime = false;
            },
            selectDate(flag) {
                this.showSelectTime = true;
                this.isReadOnly = true;
                this.currentSelect = flag;
                let nowDate = new Date();
                if (flag == '3') {
                    this.startTimeValue = this.timeFormate(new Date(nowDate - 3 * 24 * 3600 * 1000));
                    this.endTimeValue = this.timeFormate(nowDate);
                } else if (flag == '7') {
                    this.startTimeValue = this.timeFormate(new Date(nowDate - 7 * 24 * 3600 * 1000));
                    this.endTimeValue = this.timeFormate(nowDate);
                }else {
                    this.isReadOnly = false;
                }
            },
            timeFormate(date) {
                let _date = new Date(date);
                let year = _date.getFullYear();
                let month = _date.getMonth() + 1;
                let day = _date.getDate();
                return year + "-" + month + "-" + day;
            }
        },
        computed: {
            minEndTime() {
                return this.startTimeValue ? new Date(this.startTimeValue) : new Date()
            }
        }
    }
</script>
<style>
    .searchForDate {
        z-index: 1000;
        width: 90%;
        height: 11rem;
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        margin: auto;
        transform: translate3d(0, 0, 0);
        padding: 1.5rem 0.5rem 0.5rem;
    }

    .optionBtns {
        position: absolute;
        bottom: 0;
        left: 0;
        width: 100%;
        padding: 0.5rem;
        display: flex;
        justify-content: space-between;
    }

    .optionBtns .van-button {
        width: 48%;
    }
</style>