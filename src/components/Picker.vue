<template>
    <van-popup v-model="show" position="bottom" @click-overlay="onCancel">
        <van-picker show-toolbar :columns="types" @confirm="onConfirm" @cancel="onCancel" :default-index="index"/>
    </van-popup>
</template>
<script>
    // @ is an alias to /src
    import { Popup, Picker } from 'vant';
    export default {
            name: 'Picker',
            components: {
                [Popup.name]: Popup,
                [Picker.name]: Picker
            },
            props: ['types', 'showPicker', 'name', 'index'],
            data() {
                return {
                    // show: this.showPicker
                }
            },
            methods: {
                onConfirm(value,index) {
                    console.log(value);
                    console.log(index);
                    
                    this.$emit("confirm", this.name, value, index)
                },
                onCancel() {
                    this.$emit("hidePicker")
                }
            },
            computed: {
                show: {
                    get() {
                        return this.showPicker;
                    },
                    set() {
                        return this.showPicker;
                    }
                }
            }
    }
</script>