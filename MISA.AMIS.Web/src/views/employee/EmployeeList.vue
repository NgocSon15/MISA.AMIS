<template>
    <div class="employee-content">
        <div class="content-header">
            <div class="title">
                <div class="title-name">Nhân viên</div>
                <a href="" class="category-link">Tất cả danh mục</a>
            </div>
            <button class="btn-add" @click="btnAddOnClick">Thêm</button>
        </div>
        <div class="main-content">
            <div class="filter">
                <input type="text" class="text-box" placeholder="Tìm theo mã, tên nhân viên" @input="searchEmployee" v-model="searchKey">
                <div class="icon-search"></div>
            </div>
            <div class="employee-grid">
                <table cellspacing="0">
                    <thead>
                        <th style="border-left: none; max-width: 150px">MÃ NHÂN VIÊN</th>
                        <th style="max-width:150px">TÊN NHÂN VIÊN</th>
                        <th style="max-width:200px">CHỨC DANH</th>
                        <th style="max-width:200px">TÊN ĐƠN VỊ</th>
                        <th style="max-width:200px">SỐ TÀI KHOẢN</th>
                        <th style="max-width:150px">TÊN NGÂN HÀNG</th>
                        <th style="max-width:150px">TRẠNG THÁI</th>
                        <th style="max-width:150px">CHI NHÁNH</th>
                        <th style="max-width:100px">CHỨC NĂNG</th>
                    </thead>
                    <tbody>
                        <tr
                            v-for="(employee, index) in employees" :key="index"
                        >
                            <td style="border-left: none; max-width:150px">{{employee.employeeCode}}</td>
                            <td style="max-width:150px">{{employee.fullName}}</td>
                            <td style="max-width:200px">{{employee.position}}</td>
                            <td style="max-width:200px">{{employee.departmentName}}</td>
                            <td style="max-width:200px">{{employee.bankAccountNumber}}</td>
                            <td style="max-width:150px">{{employee.bankName}}</td>
                            <td style="max-width:150px">Đang sử dụng</td>
                            <td style="max-width:150px">{{employee.bankBranch}}</td>
                            <td style="max-width:100px; display:flex; align-items: center; justify-content:center; overflow: visible">
                                <button class="btn-fix" :id="employee.employeeId" @click="btnUpdateOnClick(employee.employeeId)">Sửa</button>
                                <div class="dropdown">
                                    <button class="btn-drop"></button>
                                    <div class="dropdown-content">
                                        <button class="dropdown-option">Nhân bản</button>
                                        <br>
                                        <button class="dropdown-option" @click="btnDeleteOnClick(employee.employeeId)">Xoá</button>
                                        <br>
                                        <button class="dropdown-option">Ngừng sử dụng</button>
                                    </div>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="paging-bar">
                <div class="left-bar">Tổng số: <b>200</b> bản ghi</div>
                <div class="right-bar">
                    <select class="selector">
                        <option value="">20 bản ghi trên 1 trang</option>
                    </select>
                    <button class="btn-number">Trước</button>
                    <button class="btn-number">1</button>
                    <button class="btn-number">2</button>
                    <button class="btn-number">3</button>
                    <button class="btn-number">4</button>
                    <button class="btn-number">Sau</button>
                </div>
            </div>
        </div>
        <Dialog @closeDialog="closeDialog" :value="this.dialogValue" :id="this.dialogId" :isHide="isHideDialog"/>
        <PopUp @closePopUp="closePopUp" :id="this.idDelete" :isHide="isHidePopUp"/>
    </div>
</template>

<script>
import * as axios from "axios";
import Dialog from './EmployeeDialog.vue';
import PopUp from './EmployeePopUp.vue';

export default {
    name: "Employees",
    components: {
        Dialog,
        PopUp
    },
    data() {
        return {
            employees: [],
            isHideDialog: true,
            isHidePopUp: true,
            searchKey: '',
            idDelete: '',
            dialogValue: '',
            dialogId: '',
        }
    },
    methods: {
        async btnAddOnClick() {
            this.dialogId = 'add';
            await this.getMaxEmployeeCode();
            await this.$children[0].getEmployeeCode();
            this.isHideDialog = false;
        },
        async btnUpdateOnClick(value) {
            this.dialogId = 'update';
            await this.getUpdateId(value);
            await this.$children[0].getData();
            this.isHideDialog = false;
        },
        btnDeleteOnClick(id) {
            this.idDelete = id;
            this.isHidePopUp = false;
        },
        closePopUp(value) {
            this.isHidePopUp = value;
            this.loadData();
        },
        closeDialog(value) {
            this.isHideDialog = value;
            this.loadData();
        },
        async loadData() {
            const response = await axios.get("http://localhost:56784/api/v1/Employees");
            this.employees = response.data;
        },
        async searchEmployee() {
            if (this.searchKey != null && this.searchKey != "")
            {
                const response = await axios.get("http://localhost:56784/api/v1/Employees/search?searchKey=" + this.searchKey);
                this.employees = response.data;
            }
            else
            {
                this.loadData();
            }
        },
        async getMaxEmployeeCode() {
            var response = await axios.get("http://localhost:56784/api/v1/Employees");
            var codes = [];
            var maxCode = 0;
            response.data.forEach(element => {
                codes.push(element.employeeCode);
            });
            codes.forEach(element => {
                var num = element.substring(2);
                if (num >= maxCode) {
                    maxCode = Number(num) + 1;
                }
            });
            this.dialogValue = 'NV' + maxCode;
        },
        getUpdateId(value) {
            this.dialogValue = value;
        }
    },
    async created() {
        this.loadData();
    }
}
</script>

<style scoped>
    .employee-content .content-header {
        display: flex;
        height: 80px;
        align-items: center;
    }

        .employee-content .content-header .title .title-name {
            font-size: 20px;
            font-weight: bold;
        }

        .employee-content .content-header .title .category-link {
            color: #4682b4;
            text-decoration: none;
        }

    .employee-content .content-header .btn-add {
        position: absolute;
        right: 16px;
        height: 32px;
        border-radius: 16px;
        background-color: #019160;
        color: #ffffff;
        border: none;
        outline: none;
        padding-left: 12px;
        padding-right: 12px;
        cursor: pointer;
    }

        .employee-content .content-header .btn-add:hover{
            background-color: #2fbe8e;
        }

    .main-content {
        height: calc(100vh - 168px);
        width: calc(100% - 32px);
        background-color: #ffffff;
        border-radius: 5px;
        padding: 16px 16px 0 16px;
    }

    .main-content .employee-grid {
        height: calc(100% - 98px);
        margin-top: 20px;
        overflow: auto;
    }

        .main-content .employee-grid table{
            border-collapse: collapse;
            width: 100%;
            height: 100%;
            border: none;
            text-transform: uppercase;
        }

        .main-content .employee-grid th{
            padding: 8px;
            border-bottom: 1px solid #e5e5e5;
            background-color: #eeeeee;
            border-left: 1px solid #e5e5e5;
            text-align: left;
            height: 32px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .main-content .employee-grid td{
            padding: 8px;
            border-bottom: 1px solid #e5e5e5;
            border-left: 1px solid #e5e5e5;
            height: 40px;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }

        .main-content .employee-grid tr{
            max-height: 56px;
        }

        .main-content .employee-grid tr:nth-child(2n+1) {
            background-color: #fafafa;
        }

    .main-content .paging-bar {
        height: 44px;
        display: flex;
        align-items: center;
    }

        .main-content .paging-bar .left-bar {
            position: absolute;
        }

        .main-content .paging-bar .right-bar{
            position: absolute;
            right: 32px;
        }
        
            .main-content .paging-bar .right-bar .selector{
                width: 200px;
                border: 1px solid #e5e5e5;
                height: 32px;
                padding-left: 12px;
                border-radius: 5px;
                outline: none;
                margin-right: 12px;
            }

            .main-content .paging-bar .right-bar .btn-number{
                border: none;
                outline: none;
                background-color: #ffffff;
                cursor: pointer;
                height: 20px;
                border-radius: 5px;
            }

            .main-content .paging-bar .right-bar .btn-number:hover{
                background-color: #e5e5e5;
            }

            .main-content .paging-bar .right-bar .btn-number:focus{
                border: 1px solid #000000;
            }

    .btn-fix{
        color: #4682b4;
        cursor: pointer;
        border: none;
        outline: none;
        background: none;
    }

        .btn-fix:hover{
            text-decoration: underline;
        }

    .btn-drop{
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -892px -358px;
        width: 24px;
        height: 20px;
        border: none;
        outline: none;
        cursor: pointer;
    }

    .dropdown {
        position: relative;
        display: inline-block;
    }

    .dropdown-content {
        display: none;
        right: 0;
        position: absolute;
        background-color: #f9f9f9;
        min-width: 120px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        z-index: 1;
        border: 1px solid #bbbbbb
    }

        .dropdown:hover .dropdown-content{
            display: block !important;
            position:absolute;
        }

        .dropdown:hover .btn-drop{
            background-color: #e5e5e5;
        }

    .dropdown-content .dropdown-option {
        width: 100%;
        height: 32px;
        text-align: left;
        padding-left: 12px;
        border: none;
        outline: none;
        background-color: #ffffff;
        cursor: pointer;
    }

    .dropdown-content .dropdown-option:hover {
        background-color: #e5e5e5;
        color: #019160;
    }
</style>