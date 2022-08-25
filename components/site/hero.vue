<template>
    <div class="home-hero-bg" id="inicio">
        <div class="container">
            <div class="home-hero-content">
                <div class="row">
                    <div class="col-md-6 col-xs-12">
                        <div>
                            <img src="~/assets/images/hero-bg-effect-1.png" alt="efeito" />
                        </div>
                        <div class="home-hero-text-call">
                            <b>Seja instrutor na sua região e ministre os melhores cursos de Segurança do Trabalho!</b>
                        </div>
                        <div class="home-hero-text-message">Por ser uma exigência legal, ter funcionários treinados em Segurança do Trabalho é uma necessidade crescente das empresas!</div>
                        <div class="home-hero-text-register">
                            <div class="register-menu">
                                <ul>
                                    <li><span class="register-default-color c-pointer" :class="homeIsRegister == true ? 'active' : ''" @click="homeFormType('register')">Cadastrar</span></li>
                                    <li v-if="showLoginOk" ><span class="register-default-color c-pointer" :class="homeIsRegister == false ? 'active' : ''" @click="homeFormType('login')">Fazer Login</span></li>
                                </ul>
                            </div>
                            <div class="register-content" v-if="homeIsRegister">
                                <div class="row">
                                    <div class="col-md-7 col-xs-12">
                                        <label class="label">Digite seu Nome</label>
                                        <input class="form-control" type="text" placeholder="Digite seu Nome" v-model="usName" />
                                    </div>
                                    <div class="col-md-5 col-xs-12 btn-register-base">
                                        <button class="btn btn-grey btn-register" @click="siteRegister">Cadastrar</button>
                                    </div>
                                </div>
                            </div>
                            <div class="register-content" v-else>
                                <div class="row">
                                    <div class="col-md-6 col-xs-12">
                                        <label class="label">Login</label>
                                        <input class="form-control" type="text" placeholder="Login" />
                                    </div>                                   
                                    <div class="col-md-6 col-xs-12">
                                        <label class="label">Senha</label>
                                        <input type="password" class="form-control" placeholder="Senha" />
                                    </div>
                                     <div class="col-md-12 col-xs-12 btn-register-base">
                                        <button class="btn btn-grey btn-register">Entrar</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-md-6"></div>
                </div>
            </div>
        </div>
    </div>
    <SiteRegisterForm v-if="showForm" :usName="usName" />
</template>

<script>
export default {
    data() {
        return {
            homeIsRegister: true,
            showForm: false,
            usName: ''
        }
    },
    methods: {
        async closeModal() {
            this.showForm = false
        },
        homeFormType(type) {
            if (type == 'register') {
                this.homeIsRegister = true
            } else {
                this.homeIsRegister = false
            }
        },
        siteRegister() {
            this.showForm = true
        }
    }
}
</script> 

<style lang="scss" scoped>
.home-hero-bg {
    background: url(~/assets/images/hero-bg.jpg) no-repeat center top;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    .container {
        padding-top: 220px;
    }
    .home-hero-content {
        
        .home-hero-text-call {
            font-size: 50px;
            color: #1e5083;
        }

        .home-hero-text-message {
            max-width: 350px;
            padding-top: 30px;
            font-size: 14px;
            color: #868c96;
        }
        .home-hero-text-register {
            margin-top: 120px;
            .register-menu {
                ul {
                    li {
                        display: inline-block;
                        margin-right: 35px;
                        font-weight: bold;
                        font-size: 22px;
                        &::after {
                            content: '';
                            width: 40px;
                            height: 4px;
                            background-color: rgba($color: #fff, $alpha: 0);
                            left: 0;
                            position: relative;
                            display: block;
                            top: 10px;
                        }

                        .active {
                            color: #000;
                            &::after {
                                content: '';
                                width: 50px;
                                height: 5px;
                                background-color: #8de4ff;
                                left: calc(50% - 25px);
                                position: relative;
                                display: block;
                                top: 10px;
                            }
                        }
                    }
                }
                .register-default-color {
                    color: #868c96;
                }
            }

            .register-content {
                border-radius: 15px;
                -webkit-box-shadow: 5px 4px 13px -4px #919191;
                box-shadow: 5px 4px 13px -4px #919191;
                background: #fff;
                color: #000;
                margin: 45px 0;
                padding: 20px;
               
                .btn-register-base {
                    padding-top: 20px;
                    text-align: right;
                }
                .btn-register {
                    padding: 16px 25px;
                    font-size: 22px;
                    font-weight: 600;
                }
                .form-control {
                padding-left: 8px;
                color: #868c96 !important;
                font-size: 18px;

                &::placeholder {
                    /* Chrome, Firefox, Opera, Safari 10.1+ */
                    color: #868c96;
                    opacity: 1; /* Firefox */
                    font-size: 16px;
                }

                &:-ms-input-placeholder {
                    /* Internet Explorer 10-11 */
                    color: #868c96;
                    font-size: 16px;
                }

                &::-ms-input-placeholder {
                    /* Microsoft Edge */
                    color: #868c96;
                    font-size: 16px;
                }
            }

            .label {
                color: #4293cd;
                font-weight: 600;
                padding-bottom: 5px;
            }
            }
        }
    }
}

@media (max-width: 900px) {
    .home-hero-bg {
        background: none;
    }

    .btn-register-base {        
        text-align: center !important;
    }
}
</style>