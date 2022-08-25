<template>
    <div class="layout-page" :class="!topOfPage == true ? 'scrolled' : ''">
        <div class="row">
            <div class="container">
                <div class="row">
                    <div class="col-md-1 col-xs-1 w-m-180">
                        <NuxtLink @click="topNav('#inicio')"><img src="~/assets/images/logo.png" alt="Nossa Logo" /></NuxtLink>
                    </div>
                    <div class="col-xs">
                        <nav class="top-menu">
                            <ul>
                                <li><NuxtLink @click="topNav('#inicio')">Início </NuxtLink></li>
                                <li><NuxtLink @click="topNav('#vantagens')">Vantagens</NuxtLink></li>
                                <li><NuxtLink @click="topNav('#como-funciona')">Como Funciona</NuxtLink></li>
                                <li><NuxtLink @click="topNav('#sobre-nos')">Sobre Nós</NuxtLink></li>
                                <li><NuxtLink @click="topNav('#estatisticas')">Estatísticas</NuxtLink></li>
                                <li><NuxtLink @click="topNav('#contato')">Contato</NuxtLink></li>
                            </ul>
                        </nav>
                        <div class="mobile-button" @click="checkShowMenu">
                            <div class="first"></div>
                            <div class="default"></div>
                            <div class="default"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="cel-panel-base" v-if="showMenu">
            <div class="cel-panel">
                <div class="row">
                    <div class="col-xs text-left">
                        <NuxtLink @click="topNav('#inicio')"><img src="~/assets/images/logo.png" alt="Nossa Logo" height="70" /></NuxtLink>
                    </div>
                    <div class="col-md-1">
                        <h4 @click="checkShowMenu" class="c-pointer">
                            <img src="~/assets/icons/close-modal.png" />
                        </h4>
                    </div>
                </div>
                <hr />
                <div class="mobile-menu">
                    <ul>
                        <li><NuxtLink @click="topNav('#inicio')">Início </NuxtLink></li>
                        <li><NuxtLink @click="topNav('#vantagens')">Vantagens</NuxtLink></li>
                        <li><NuxtLink @click="topNav('#como-funciona')">Como Funciona</NuxtLink></li>
                        <li><NuxtLink @click="topNav('#sobre-nos')">Sobre Nós</NuxtLink></li>
                        <li><NuxtLink @click="topNav('#estatisticas')">Estatísticas</NuxtLink></li>
                        <li><NuxtLink @click="topNav('#contato')">Contato</NuxtLink></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            topOfPage: true,
            showMenu: false
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll)
    },
    mounted() {
        this.handleScroll()
    },
    methods: {
        checkShowMenu() {
            if (this.showMenu) {
                this.showMenu = false
            } else {
                this.showMenu = true
            }
        },
        checkPosition() {
            alert(document.body.getBoundingClientRect().top)
        },
        topNav(toComponent) {
            this.scrollTo(toComponent)
            if (this.showMenu) {
                this.showMenu = false
            }
        },
        scrollTo: function (hash) {
            setTimeout(() => {
                location.href = hash
            }, 1)
        },
        handleScroll() {
            if (window.pageYOffset > 100) {
                if (this.topOfPage) {
                    this.topOfPage = false
                }
            } else {
                if (!this.topOfPage) {
                    this.topOfPage = true
                }
            }
        }
    }
}
</script> 



<style lang="scss" scoped>
.scrolled {
    background: #ffffff;
    padding-top: 0 !important;
    -webkit-box-shadow: -3px 5px 16px -6px #949494;
    box-shadow: -3px 5px 16px -6px #949494;
}
.layout-page {
    position: fixed;
    width: 100%;
    padding-top: 35px;
    z-index: 999999999;

    .mobile-button {
        width: 40px;
        height: 40px;
        float: right;
        margin-top: 20px;
        display: none;
        .first {
            height: 1px;
            border: 2px solid #000;
            width: 45%;
            margin: 8px 0;
        }

        .default {
            height: 1px;
            border: 2px solid #000;
            width: 100%;
            margin: 8px 0;
        }
    }
    .w-m-180 {
        min-width: 190px;
    }
    .top-menu {
        color: #fff;
        ul {
            text-align: right;
            li {
                font-weight: 500;
                color: #000;
                display: inline-block;
                padding: 26px 15px;
            }
        }
    }

    .cel-panel-base {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100vh;
        background: rgba($color: #000000, $alpha: 0.6);
        .cel-panel {
            position: absolute;
            height: 100vh;
            width: 250px;
            top: 0;
            left: 0;
            background: #fff;
            padding: 10px;
            .mobile-menu {
                color: #fff;
                ul {
                    text-align: left;
                    li {
                        font-weight: 500;
                        color: #000;
                        display: block;
                        padding: 10px 15px;
                    }
                }
            }
        }
    }

    @media (max-width: 900px) {
        .top-menu {
            display: none;
        }

        .mobile-button {
            display: block;
        }
    }

    @media (max-width: 500px) {
    }
}
</style>