<template>
    <div ref="popup" class="pop-up" :class="{isHide:isHide}">
        <div class="modal"></div>
        <div class="pop-up-main">
            <div class="pop-up-content">
                <div class="icon-alert"></div>
                <div class="alert">Bạn có thực sự muốn xóa nhân viên {{this.employeeCode}} không?</div>
            </div>
            <div class="line"></div>
            <div class="pop-up-footer">
                <button class="btn-cancel" @click="btnCancelOnClick">Không</button>
                <button class="btn-accept" @click="btnAcceptOnClick">Có</button>
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
            employeeCode: '',
        }
    },
    methods: {
        btnCancelOnClick() {
            this.$emit('closePopUp',true);
        },
        async btnAcceptOnClick() {
            await axios.delete("http://localhost:56784/api/v1/Employees/" + this.$attrs.id);
            this.$emit('closePopUp',true);
        },
        async getEmployeeCode() {
            var response = await axios.get("http://localhost:56784/api/v1/Employees/" + this.$attrs.id);
            this.employeeCode = response.data[0].employeeCode;
        }
    },
    updated() {
        this.getEmployeeCode();
        console.log(this.employeeCode);
    },
}
</script>

<style scoped>
    .isHide {
        display: none;
    }

    .modal {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
        background-color: #000000;
        opacity: 0.3;
    }

    .pop-up-main {
        width: 500px;
        background-color: white;
        position: fixed;
        left: calc(50vw - 250px);
        top: 100px;
        border-radius: 4px;
        padding: 40px 40px 12px 40px;
    }

    .pop-up-main .pop-up-content {
        display: flex;
    }

    .pop-up-main .pop-up-content .icon-alert {
        width: 40px;
        height: 40px;
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -598px -463px;
    }

    .pop-up-main .pop-up-content .alert{
        margin: 8px 0 0 16px;
        font-size: 16px;
        color: #808080;
    }

    .line {
        border-top: 1px solid #808080;
        margin-top: 40px;
    }

    .pop-up-main .pop-up-footer {
        display: flex;
        align-items: center;
        height: 80px;
    }

    .btn-cancel{
        height: 40px;
        padding: 0 16px 0 16px;
        font-weight: bold;
        cursor: pointer;
        background-color: #ffffff;
        outline: none;
        border: 1px solid #bbbbbb;
        border-radius: 4px;
    }

        .btn-cancel:hover{
            background-color: #e9ebee;
        }

    .btn-accept{
        height: 40px;
        padding: 0 16px 0 16px;
        font-weight: bold;
        cursor: pointer;
        background-color: #019160;
        outline: none;
        border: 1px solid #bbbbbb;
        border-radius: 4px;
        color: #ffffff;
        position: absolute;
        right: 40px;
    }

        .btn-accept:hover{
            background-color: #2fbe8e;
        }
</style>