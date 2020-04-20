<template>
    <van-popup duration="0" class="filter" v-model="show" position="right" :style="{ width: '80%',height: '100%' }">
        <div>
            <!-- <van-field readonly clickable name="startTime" :value="'value'" label="起始日期" placeholder="点击选择日期"
                @click="showCalendar = true" />
            <van-field readonly clickable name="endTime" :value="'value'" label="结束日期" placeholder="点击选择日期"
                @click="showCalendar = true" /> -->
            <van-field readonly clickable name="picker" :value="filterField.type.value" label="值班表类型" placeholder="点击选择值班表类型"
                @click="onShowPicker('typeList', 'type')" />
            <van-field readonly clickable name="picker" :value="filterField.mode.value" label="值班模式" placeholder="点击选择值班模式"
                @click="onShowPicker('modeList', 'mode')" />
            <van-field readonly clickable name="picker" :value="filterField.organization.value" label="机构" placeholder="点击选择机构"
                @click="onShowPicker('organizationList', 'organization')" />
            <van-field readonly clickable name="picker" :value="filterField.department.value" label="部门" placeholder="点击选择部门"
                @click="onShowPicker('departmentList', 'department')" />
            <van-field readonly clickable name="picker" :value="filterField.team.value" label="团队" placeholder="点击选择团队"
                @click="onShowPicker('teamList', 'team')" />
            <van-field readonly clickable name="picker" :value="filterField.status.value" label="条目状态" placeholder="点击选择条目状态"
                @click="onShowPicker('statusList', 'status')" />
            <van-field readonly clickable name="picker" :value="filterField.method.value" label="值班方式" placeholder="点击选择值班方式"
                @click="onShowPicker('methodList', 'method')" />
            <van-field readonly clickable name="picker" :value="filterField.role.value" label="值班角色" placeholder="点击选择值班角色"
                @click="onShowPicker('roleList', 'role')" />
            <picker :name="filedName" :index="filedIndex" :types="pickColumns" :showPicker="showPicker" @confirm="onConfirm" @hidePicker="onHidePicker"></picker>


            <div class="optionBtns">
                <van-button @click="onReset">重置</van-button>
                <van-button type="primary" @click="onFilter">确定</van-button>
            </div>
        </div>
    </van-popup>
</template>
<script>
    // @ is an alias to /src
    import { Button, Col, Row, Popup, Field, Calendar } from 'vant';
    import Picker from "./Picker"

    export default {
        name: 'SearchForDate',
        components: {
            [Button.name]: Button,
            [Col.name]: Col,
            [Row.name]: Row,
            [Popup.name]: Popup,
            [Field.name]: Field,
            [Calendar.name]: Calendar,
            Picker
        },
        data() {
            return {
                show: false,
                showCalendar: true,
                showPicker: false,
                pickColumns: [],
                filedName: '',
                filedIndex: '',
                typeList: ['a','b'],  //值班表类型
                modeList: ['c', 'd'],  //值班模式
                organizationList: ['总行', '分行'], //机构
                departmentList: ['信息科技运营中心', '软件中心'], //部门
                teamList: ["系统管理一", "系统管理二"],
                statusList: ["已发布", "未发布"],
                methodList: ["带班", "现场"],
                roleList: ["变更经理", "一线"]
            }
        },
        created() {
            this.filterDataInit();
        },
        methods: {
            filterDataInit() {
                this.filterField = {
                    type: { },
                    mode: { },
                    organization: { },
                    department: { },
                    team: { },
                    status: { },
                    method: { },
                    role: { }
                }
            },
            showFilter() {
                this.show = true;
            },
            onShowPicker(attr, name) {
                this.pickColumns = [...this[attr]];
                this.filedName = name;
                this.filedIndex = this.filterField[name].index;
                this.showPicker = true;
            },
            onConfirm(name, value, index) {
                this.filterField[name].value = value;                
                this.filterField[name].index = index;                
                this.showPicker = false;
            },
            onHidePicker() {
                this.showPicker = false;
            },
            onReset() {
                this.filterDataInit();
                this.show = false;
                console.log('reset', this.filterField);
                this.$emit("filterData", this.filterField);
            },
            onFilter() {
                console.log('filter', this.filterField);
                this.show = false;
                this.$emit("filterData", this.filterField);
            }
        }
    }
</script>
<style>
    .filter {
        z-index: 1000;
        width: 80%;
        height: 100%;
        position: absolute;
        /* left: 0; */
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