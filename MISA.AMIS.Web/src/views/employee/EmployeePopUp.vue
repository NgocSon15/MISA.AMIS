<template>
    <div ref="popup" class="pop-up" :class="{isHide:isHide}">
        <div class="modal"></div>
        <div class="pop-up-main">
            <div class="pop-up-delete" :class="{isHide:hideDelete}">
                <div class="pop-up-content">
                    <div class="icon-alert"></div>
                    <div class="alert">{{this.alertMsg}}</div>
                </div>
                <div class="line"></div>
                <div class="pop-up-footer">
                    <button class="btn-cancel" @click="btnCancelOnClick">Không</button>
                    <button class="btn-accept" @click="btnAcceptOnClick">Có</button>
                </div>
            </div>
            <div class="pop-up-alert" :class="{isHide:hideAlert}">
                <div class="pop-up-content">
                    <div class="icon-alert"></div>
                    <div style="display: block;">
                        <div class="alert"
                            v-for="(alert, index) in this.alertMsg" :key="index"
                        >
                        {{alert}}
                        </div>
                    </div>
                </div>
                <div class="line"></div>
                <div class="pop-up-footer">
                    <button class="btn-accept" @click="btnCancelOnClick">Ok</button>
                </div>
            </div>
            <div class="pop-up-success" :class="{isHide:hideSuccess}">
                <div class="pop-up-content">
                    <div class="icon-success"></div>
                    <div class="alert">{{this.successMsg}}</div>
                </div>
                <div class="line"></div>
                <div class="pop-up-footer">
                    <button class="btn-accept" @click="btnOkOnClick">Ok</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import * as axios from 'axios';

export default {
    props: ['isHide'],
    data() {
        return {
            employeeId: '',
            hideDelete: true,
            hideAlert: true,
            hideSuccess: true,
            alertMsg: [],
            successMsg: '',
        }
    },
    methods: {
        // đóng pop up
        btnCancelOnClick() {
            this.$emit('closePopUp',true);
        },

        // thực hiện nhân viên khỏi hệ thống khi nhấn nút đồng ý xóa
        async btnAcceptOnClick() {
            await axios.delete("http://localhost:56784/api/v1/Employees/" + this.employeeId);
            this.$emit('closePopUp',true);
        },

        // đóng pop up thông báo đồng thời đóng form nhân viên
        btnOkOnClick() {
            this.$emit('closePopUp',true);
            this.$parent.btnCancelOnClick();
        },
    },
}
</script>

<style scoped>
@import url("../../style/page/employee/employeepopup.css");
</style>