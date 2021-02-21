<template>
    <div class="header">
        <div class="left-header">
            <select class="select">
                <option>CÔNG TY TNHH NƯỚC UỐNG TINH KHIẾT SÀI GÒN</option>
            </select>
        </div>
        <div class="right-header">
            <div class="filter">
                <input type="text" class="text-box" placeholder="Nhập từ khóa tìm kiếm">
                <div class="icon-search"></div>
            </div>
            <div class="header-icon icon-more"></div>
            <div class="header-icon icon-setting"></div>
            <div class="header-icon icon-message"></div>
            <div class="header-icon icon-help"></div>
            <div class="header-icon icon-notification"></div>
            <div class="user-profile">
                <div class="avatar"></div>
                <div class="user-name">Nguyễn Ngọc Sơn</div>
                <div class="icon-dropdown"></div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .header {
        position: absolute;
        left: 200px;
        height: 60px;
        width: calc(100% - 200px);
        display: flex;
        align-items: center;
    }

        .header .left-header{
            position: absolute;
            left: 10px;
        }

            .header .left-header .select {
                height: 40px;
                font-weight: bold;
                font-size: 16px;
                outline: none;
                border: none;
                border-radius: 5px;
                cursor: pointer;
            }

            .header .left-header .select:hover {
                background-color: #e5e5e5;
            }

        .header .right-header {
            position: absolute;
            right: 24px;
            display: flex;
            align-items: center;
        }

        .header .right-header .header-icon{
            width: 24px;
            height: 24px;
            background-repeat: no-repeat;
            margin-right: 16px;
        }

        .header .right-header .user-profile{
            display: flex;
            align-items: center;
            height: 32px;
            cursor: pointer;
        }

            .header .right-header .user-profile .avatar{
                height: 32px;
                width: 32px;
                border-radius: 50%;
                background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -352px -894px;
                margin-right: 10px;
            }

            .header .right-header .user-profile .user-name{
                font-weight: bold;
                margin-right: 10px;
            }

            .header .right-header .user-profile .icon-dropdown{
                width: 9px;
                height: 6px;
                background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -1078px -38px;
            }

    .icon-more {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -568px -30px;
    }

    .icon-setting {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -676px -30px;
    }

    .icon-message {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -899px -30px;
    }

    .icon-help {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -732px -31px;
    }

    .icon-notification {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -788px -30px;
    } 
</style>