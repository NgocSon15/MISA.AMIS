<template>
    <div 
        class="employee-dialog"
        title="Thông tin nhân viên"
        :class="{isHide:isHide}"
    >
        <div class="modal"></div>
        <div class="dialog">
            <div class="dialog-header">
                <div class="dialog-title">Thông tin nhân viên</div>
                <label class="checkbox-container">
                    <input type="checkbox" class="checkbox">
                    Là khách hàng
                </label>
                <label class="checkbox-container">
                    <input type="checkbox" class="checkbox">
                    Là nhà cung cấp
                </label>
                <button class="btn-close" @click="btnCancelOnClick"></button>
                <button class="btn-help"></button>
            </div>
            <div class="dialog-content">
                <div class="top-content">
                    <div class="topleft-content">
                        <div style="display:flex">
                            <div style="margin-right: 12px">
                                <label><b>Mã</b> <font color="red">*</font></label>
                                <br>
                                <input type="text" class="text-field" style="width:184px" v-model="employee.employeeCode" required>
                            </div>
                            <div>
                                <label><b>Tên</b> <font color="red">*</font></label>
                                <br>
                                <input type="text" class="text-field" style="width:242px" v-model="employee.fullName" autofocus required>
                            </div>
                        </div>
                        <div>
                            <label><b>Đơn vị</b> <font color="red">*</font></label>
                            <br>
                            <select class="select-field" v-model="employee.departmentId">
                                <option value="4e272fc4-7875-78d6-7d32-6a1673ffca7c" selected>PHÒNG NHÂN SỰ</option>
                                <option value="11452b0c-768e-5ff7-0d63-eeb1d8ed8cef">PHÒNG ĐÀO TẠO</option>
                                <option value="142cb08f-7c31-21fa-8e90-67245e8b283e">PHÒNG CÔNG NGHỆ</option>
                                <option value="17120d02-6ab5-3e43-18cb-66948daf6128">PHÒNG MARKETING</option>
                                <option value="469b3ece-744a-45d5-957d-e8c757976496">PHÒNG HÀNH CHÍNH</option>
                            </select>
                        </div>
                        <div>
                            <label><b>Chức danh</b></label>
                            <br>
                            <input type="text" class="text-field" v-model="employee.position">
                        </div>
                    </div>
                    <div class="topright-content">
                        <div style="display:flex">
                            <div style="margin-right: 16px;">
                                <label><b>Ngày sinh</b></label>
                                <br>
                                <input type="date" class="text-field" style="width:184px; height:36px" v-model="employee.dateOfBirth">
                            </div>
                            <div>
                                <label><b>Giới tính</b></label>
                                <br>
                                <div class="radio-field">
                                    <label class="radio-container">
                                        Nam
                                        <input type="radio" name="gender" value="0" v-model="employee.gender">
                                        <span class="checkmark"></span>
                                    </label>
                                    <label class="radio-container">
                                        Nữ
                                        <input type="radio" name="gender" value="1" v-model="employee.gender">
                                        <span class="checkmark"></span>
                                    </label>
                                    <label class="radio-container">
                                        Khác
                                        <input type="radio" name="gender" value="2" v-model="employee.gender">
                                        <span class="checkmark"></span>
                                    </label>
                                </div>
                            </div>
                        </div>
                        <div style="display:flex">
                            <div style="margin-right: 12px">
                                <label><b>Số CMND</b></label>
                                <br>
                                <input type="text" class="text-field" style="width:242px" v-model="employee.identityNumber">
                            </div>
                            <div>
                                <label><b>Ngày cấp</b></label>
                                <br>
                                <input type="date" class="text-field" style="width:184px; height: 36px" v-model="employee.identityDate">
                            </div>
                        </div>
                        <div>
                            <label><b>Nơi cấp</b></label>
                            <br>
                            <input type="text" class="text-field" v-model="employee.identityPlace">
                        </div>
                    </div>
                </div>
                <div class="bottom-content">
                    <div class="navigator">
                        <button class="btn-navigate" :class="{isChosen:hideBankAccount}" @click="btnContactOnClick">Liên hệ</button>
                        <button class="btn-navigate" :class="{isChosen:hideContact}" @click="btnBankAccountOnClick">Tài khoản ngân hàng</button>
                    </div>
                    <div class="information-field">
                        <div class="contact" :class="{isHide:hideContact}">
                            <div>
                                <label><b>Địa chỉ</b></label>
                                <br>
                                <input type="text" class="text-field" style="width: 920px;" v-model="employee.address">
                            </div>
                            <div style="display: flex">
                                <div style="margin-right: 12px;">
                                    <label><b>ĐT di động</b></label>
                                    <br>
                                    <input type="text" class="text-field" style="width: 220px;" v-model="employee.phoneNumber">
                                </div>
                                <div style="margin-right: 12px;">
                                    <label><b>ĐT cố định</b></label>
                                    <br>
                                    <input type="text" class="text-field" style="width: 220px;" v-model="employee.homeNumber">
                                </div>
                                <div>
                                    <label><b>Email</b></label>
                                    <br>
                                    <input type="text" class="text-field" style="width: 220px;" v-model="employee.email">
                                </div>
                            </div>
                        </div>
                        <div class="bank-account" :class="{isHide:hideBankAccount}">
                            <table cellspacing="0">
                                <thead>
                                    <th style="border-left: none; width: 200px">SỐ TÀI KHOẢN</th>
                                    <th style="width: 250px">TÊN NGÂN HÀNG</th>
                                    <th style="width: 200px">CHI NHÁNH</th>
                                    <th style="width: 250px">TỈNH/TP CỦA NGÂN HÀNG</th>
                                    <th style="border-right: none; width: 34px"></th>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td style="border-left: none; width: 200px">
                                            <input type="text" class="table-input" v-model="employee.bankAccountNumber">
                                        </td>
                                        <td style="width: 250px">
                                            <input type="text" class="table-input" v-model="employee.bankName">
                                        </td>
                                        <td style="width: 200px">
                                            <input type="text" class="table-input" v-model="employee.bankBranch">
                                        </td>
                                        <td style="width: 250px">
                                            <input type="text" class="table-input" v-model="employee.bankPlace">
                                        </td>
                                        <td style="border-right: none; width: 34px">
                                            <button class="btn-recycle-bin"></button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                            <div style="display: flex; margin-top: 12px;">
                                <button class="btn-table">Thêm dòng</button>
                                <button class="btn-table">Xóa hết dòng</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="underline"></div>
            <div class="dialog-footer">
                <button class="btn-cancel" @click="btnCancelOnClick">Hủy</button>
                <button class="btn-save" @click="btnSaveOnClick">Cất và thêm</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    props: ['isHide'],
    data() {
        return {
            hideContact: false,
            hideBankAccount: true,
            employee: {
                address: null,
                bankAccountNumber: null,
                bankBranch: null,
                bankName: null,
                bankPlace: null,
                dateOfBirth: null,
                departmentId: "4e272fc4-7875-78d6-7d32-6a1673ffca7c",
                departmentName: null,
                email: null,
                employeeCode: "",
                fullName: "",
                gender: null,
                homeNumber: null,
                idEmployee: null,
                identityDate: null,
                identityNumber: null,
                identityPlace: null,
                phoneNumber: null,
                position: null,
            }
        }
    },
    methods: {
        btnCancelOnClick() {
            this.$emit('closeDialog',true);
        },

        btnContactOnClick() {
            this.hideContact = false;
            this.hideBankAccount = true;
        },

        btnBankAccountOnClick() {
            this.hideContact = true;
            this.hideBankAccount = false;
        },

        async getData() { 
            var response = await axios.get("http://localhost:56784/api/v1/Employees/" + this.$attrs.value);
            this.employee = response.data[0];
        },

        getEmployeeCode() {
            this.employee.employeeCode = this.$attrs.value;
        },

        async btnSaveOnClick() {
            await axios.post("http://localhost:56784/api/v1/Employees", this.employee)
            .then((response) => {
                alert(response.data);
            }, (error) => {
                alert(error.response.data.userMsg);
            });
        },
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

    .dialog {
        position: fixed;
        left: calc(50vw - 400px);
        top: 80px;
        width: 1000px;
        background-color: white;
    }

        .dialog .dialog-header {
            display: flex;
            height: 60px;
        }

            .dialog .dialog-header .dialog-title {
                font-size: 20px;
                font-weight: bold;
                margin-top: 20px;
                margin-left: 20px;
                margin-right: 20px;
            }

            .dialog .dialog-header .checkbox-container{
                color: #808080;
                margin-top: 8px;
                font-size: 16px;
                display: flex;
                align-items: center;
                margin-right: 16px;
            }

                .dialog .dialog-header .checkbox-container .checkbox{
                    width: 20px;
                    height: 20px;
                    margin-right: 8px;
                }

            .dialog .dialog-header .btn-close{
                position: absolute;
                right: 0;
                height: 40px;
                width: 40px;
                background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -136px -136px;
                border: none;
                outline: none;
                cursor: pointer;
            }

                .dialog .dialog-header .btn-close:hover{
                    background-color: #e5e5e5;
                }

            .dialog .dialog-header .btn-help{
                position: absolute;
                right: 40px;
                height: 32px;
                width: 32px;
                border-radius: 50%;
                background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -84px -140px;
                border: none;
                outline: none;
                cursor: pointer;
                margin-top: 4px;
            }

                .dialog .dialog-header .btn-help:hover{
                    background-color: #e5e5e5;
                }

        .dialog .dialog-content {
            padding: 0 20px 0 20px;
        }

            .dialog .dialog-content .top-content {
                display: flex;
            }

                .dialog .dialog-content .top-content .topleft-content {
                    margin-right: 20px;
                }

    .text-field {
        margin-top: 8px;
        margin-bottom: 16px;
        height: 34px;
        width: 454px;
        outline: none;
        border: 1px solid #bbbbbb;
        padding-left: 12px;
        font-size: 16px;
    }

        .text-field:focus {
            border-color: #019160;
        }
    
    .select-field {
        margin-top: 8px;
        margin-bottom: 16px;
        height: 38px;
        width: 470px;
        outline: none;
        border: 1px solid #bbbbbb;
        padding-left: 12px;
        font-size: 16px;
    }

        .select-field:focus {
            border-color: #019160;
        }
    
    .radio-field {
        margin-top: 8px;
        margin-bottom: 16px;
        height: 38px;
        display: flex;
        align-items: center;
        font-size: 16px;
    }

        .radio-field .radio-container {
            position: relative;
            cursor: pointer;
            padding-left: 32px;
            margin-right: 16px;
        }

            .radio-field .radio-container input {
                position: absolute;
                opacity: 0;
                cursor: pointer;
            }

            .radio-field .radio-container .checkmark {
                position:absolute;
                left: 0;
                top: 0;
                height: 24px;
                width: 24px;
                border: 1px solid #bbbbbb;
                border-radius: 50%;
            }

            .radio-field .radio-container:hover input ~ .checkmark {
                background-color: #e9ebee;
            }

            .radio-field .radio-container .checkmark:after {
                content: "";
                position: absolute;
                display: none;
            }

            .radio-field .radio-container input:checked ~ .checkmark:after {
                display: block;
            }

            .radio-field .radio-container input:checked ~ .checkmark{
                border: 1px solid #019160;
            }

            .radio-field .radio-container .checkmark:after {
                top: 4px;
                left: 4px;
                width: 16px;
                height: 16px;
                border-radius: 50%;
                background: #019160;
            }

            .dialog .dialog-content .bottom-content .navigator {
                display: flex;
            }

            .dialog .dialog-content .bottom-content .navigator .btn-navigate {
                margin-right: 4px;
                padding: 8px;
                border: 1px solid #bbbbbb;
                cursor: pointer;
                background-color: #ffffff;
                outline: none;
                border-bottom: none;
                height: 32px;
                margin-top: 8px;
                font-size: 14px;
            }

                .dialog .dialog-content .bottom-content .navigator .btn-navigate:hover {
                    background-color: #e9ebee;
                }

            .isChosen{
                background-color: #99d6ff !important;
                height: 40px !important;
                margin-top: 0px !important;
            }

            .dialog .dialog-content .bottom-content .information-field {
                height: 200px;
                border: 1px solid #bbbbbb;
                padding: 12px;
                margin-bottom: 32px;
            }

                .dialog .dialog-content .bottom-content .information-field table {
                    width: 100%;
                    border-collapse: collapse;
                }

                .dialog .dialog-content .bottom-content .information-field table th {
                    border: 1px solid #bbbbbb;
                    border-top: none;
                    text-align: left;
                    height: 40px;
                    padding-left: 12px;
                    background-color: #eeeeee;
                }

                .dialog .dialog-content .bottom-content .information-field table td {
                    border: 1px solid #e5e5e5;
                    border-top: none;
                    text-align: left;
                    height: 44px;
                    padding-left: 12px;
                }

                .dialog .dialog-content .bottom-content .information-field table tr {
                    background-color: #fafafa;
                }

                .table-input {
                    width: calc(100% - 26px);
                    height: 32px;
                    border: 1px solid #e5e5e5;
                    outline: none;
                    padding-left: 12px;
                    font-size: 16px;
                }

                    .table-input:focus {
                        border-color: #019160;
                    }

                .btn-recycle-bin {
                    background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -464px -313px;
                    width: 20px;
                    height: 20px;
                    cursor: pointer;
                    outline: none;
                    border: none;
                }

                .btn-table {
                    padding: 4px 16px 4px 16px;
                    border: 1px solid #bbbbbb;
                    outline: none;
                    cursor: pointer;
                    background-color: #ffffff;
                    border-radius: 4px;
                    margin-right: 12px;
                    font-weight: bold;
                }

                    .btn-table:hover {
                        background-color: #e9ebee;
                    }

        .dialog .underline {
            border-top: 1px solid #e5e5e5;
            margin: 0 20px 0 20px;
        }

        .dialog .dialog-footer {
            margin: 0 20px 0 20px;
            height: 80px;
            display: flex;
            align-items: center;
        }

            .dialog .dialog-footer .btn-cancel{
                height: 40px;
                padding: 0 16px 0 16px;
                font-weight: bold;
                cursor: pointer;
                background-color: #ffffff;
                outline: none;
                border: 1px solid #bbbbbb;
                border-radius: 4px;
            }

                .dialog .dialog-footer .btn-cancel:hover{
                    background-color: #e9ebee;
                }

            .dialog .dialog-footer .btn-save{
                position: absolute;
                right: 20px;
                height: 40px;
                padding: 0 16px 0 16px;
                font-weight: bold;
                cursor: pointer;
                background-color: #019160;
                outline: none;
                border: 1px solid #bbbbbb;
                border-radius: 4px;
                color: #ffffff;
            }

                .dialog .dialog-footer .btn-save:hover{
                    background-color: #2fbe8e;
                }
</style>