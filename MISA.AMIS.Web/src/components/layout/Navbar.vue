<template>
    <div class="navbar">
        <div class="logo-box">
            <div class="toggle-icon"></div>
            <div class="amis-logo"></div>
        </div>
        <div class="navbar-content">
            <button class="item"
                v-for="(item, index) in items" :key="index"
            >
                <div class="item-icon" :class="item.icon"></div>
                <div class="item-text">{{item.text}}</div>
            </button>
        </div>
    </div>
</template>

<script>
export default {
    name: "Navbar",
    data() {
        return {
            items: [
                {icon: "icon-dashboard", text: "Tổng quan"},
                {icon: "icon-cash", text: "Tiền mặt"},
                {icon: "icon-deposit", text: "Tiền gửi"},
                {icon: "icon-buy", text: "Mua hàng"},
                {icon: "icon-sell", text: "Bán hàng"},
                {icon: "icon-bill-manage", text: "Quản lý hóa đơn"},
                {icon: "icon-storage", text: "Kho"},
                {icon: "icon-tool", text: "Công cụ dụng cụ"},
                {icon: "icon-asset", text: "Tài sản cố định"},
                {icon: "icon-tax", text: "Thuế"},
                {icon: "icon-price", text: "Giá thành"},
                {icon: "icon-synthetic", text: "Tổng hợp"},
                {icon: "icon-budget", text: "Ngân sách"},
                {icon: "icon-report", text: "Báo cáo"},
                {icon: "icon-finance", text: "Phân tích tài chính"},
            ]
        }
    },
}
</script>

<style scoped>
    .navbar {
        position: relative;
        float: left;
        height: 100vh;
        width: 200px;
        background-color: #404040;
    }

        .navbar .logo-box {
            display: flex;
            align-items: center;
            padding-left: 24px;
            width: calc(100% - 24px);
            height: 60px;
            cursor: pointer;
        }

            .navbar .logo-box .toggle-icon {
                background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -428px -92px;
                width: 16px;
                height: 16px;
            }

            .navbar .logo-box .amis-logo {
                margin-left: 16px;
                height: 40px;
                width: calc(100% - 27px);
                background: url('../../assets/img/Logo_Module_TiengViet_White.66947422.svg') no-repeat;
                background-size: contain;
            }

        .navbar .navbar-content{
            width: 100%;
        }

            .navbar .navbar-content .item{
                display: flex;
                height: 44px;
                width: 100%;
                align-items: center;
                cursor: pointer;
                border: none;
                outline: none;
                background-color: #404040;
            }

            .navbar .navbar-content .item:hover{
                background-color: #595959;
            }

                .navbar .navbar-content .item .item-icon {
                    height: 20px;
                    width: 20px;
                    margin-left: 16px;
                    background-repeat: no-repeat;
                }

                .navbar .navbar-content .item .item-text {
                    margin-left: 16px;
                    color: #ffffff;
                }

    .icon-dashboard {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -31px -1587px;
    }

    .icon-cash {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -74px -1589px;
    }

    .icon-deposit {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -117px -1590px;
    }

    .icon-buy {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -161px -1589px;
    }

    .icon-sell {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -206px -1588px;
    }

    .icon-bill-manage {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -248px -1589px;
    }

    .icon-storage {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -292px -1589px;
    }

    .icon-tool {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -337px -1590px;
    }

    .icon-asset {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -379px -1589px;
    }

    .icon-tax {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -423px -1591px;
    }

    .icon-price {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -468px -1590px;
    }

    .icon-synthetic {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -509px -1590px;
    }

    .icon-budget {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -423px -1664px;
    }

    .icon-report {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -546px -1593px;
    }

    .icon-finance {
        background: url('../../assets/img/Sprites.64af8f61.svg') no-repeat -248px -1667px;
    }
</style>
