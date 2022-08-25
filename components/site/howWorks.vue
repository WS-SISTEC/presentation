<template>
    <div class="layout-howWorks" id="como-funciona">
        <div class="container">
            <div class="row">
                <div class="col-md-6 col-xs-12 how-works-mobile">
                    <div class="howWorksCall-align">
                        <div class="howWorksCall">
                            <div class="title">Como Funciona</div>
                            <div class="content">Após a aprovação do seu cadastro - feito diretamente pelo app - você
                                estará apto a ser um instrutor licenciado pelo Instituto Santa Catarina, referência
                                nacional em Segurança do Trabalho.</div>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col-xs-12">
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-register.png" /></div>
                        <div class="text">
                            <div class="title">Cadastro</div>
                            <div class="content">Preencha os dados necessários e aguarde a análise. O cadastro é simples
                                e facilitado, sem burocracia.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-download.png" /></div>
                        <div class="text">
                            <div class="title">Baixar o App</div>
                            <div class="content">Baixe nosso app na Google Play ou Apple Store.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-proficiency.png" /></div>
                        <div class="text">
                            <div class="title">Proficiência</div>
                            <div class="content">Envie os documentos que comprovam sua formação na área da Segurança do
                                Trabalho.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-proposals.png" /></div>
                        <div class="text">
                            <div class="title">Propostas</div>
                            <div class="content">Conheça as propostas de cursos na sua região de atuação e escolha
                                aquelas que mais combinam com seu perfil profissional.</div>
                        </div>
                    </div>
                    <div class="howWorks-card highlights">
                        <div class="icon"><img src="~/assets/images/icon-analysis.png" /></div>
                        <div class="text">
                            <div class="title">Analisa e Aceita</div>
                            <div class="content">Você analisa cada oportunidade e, em caso de aceitação, continuamos o
                                processo para que o treinamento aconteça.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-training.png" /></div>
                        <div class="text">
                            <div class="title">Faz o Treinamento</div>
                            <div class="content">Ministre o treinamento como um instrutor nomeado pelo Instituto Santa
                                Catarina. Você será o nosso representante na cidade/região.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-evidencies.png" /></div>
                        <div class="text">
                            <div class="title">Anexa as Evidências</div>
                            <div class="content">Anexe as evidências exigidas que comprovam a realização do treinamento.
                            </div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-certificate.png" /></div>
                        <div class="text">
                            <div class="title">Assina os Certificados</div>
                            <div class="content">Emita os Certificados fornecidos por nós e assinado por você aos alunos
                                participantes.</div>
                        </div>
                    </div>
                    <div class="howWorks-card">
                        <div class="icon"><img src="~/assets/images/icon-receive.png" /></div>
                        <div class="text">
                            <div class="title">Recebe o Pagamento</div>
                            <div class="content">Receba o pagamento direto em sua conta corrente após a conclusão do
                                curso.</div>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col-xs-12 how-works-mobile">
                    <div class="howWorksCall-align">
                        <div class="howWorksCall">
                            <div class="actions">
                                <button class="btn btn-grey btn-register " @click="siteRegister">Cadastrar</button>
                                <button class="btn btn-blue btn-login">Baixar o APP</button>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-md-6 col-xs-12 how-works-desktop">
                    <div class="howWorksCall-align">
                        <div class="howWorksCall">
                            <div class="title">Como Funciona</div>
                            <div class="content">Após a aprovação do seu cadastro - feito diretamente pelo app - você
                                estará apto a ser um instrutor licenciado pelo Instituto Santa Catarina, referência
                                nacional em Segurança do Trabalho.</div>
                            <div class="separator"></div>
                            <div class="actions">
                                <button class="btn btn-grey btn-register mr-50" @click="siteRegister">Cadastrar</button>
                                <button class="btn btn-blue btn-login">Baixar o APP</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <SiteRegisterForm v-if="showFormHowWorks" usName="" />
</template>

<script>
export default {
    data() {
        return {
            showFormHowWorks: false,
            usName: ''
        }
    },
    methods: {
        async closeModal() {
            this.showFormHowWorks = false
        },
        siteRegister() {
            this.showFormHowWorks = true
        }
    }
}
</script> 

<style lang="scss" scoped>
.layout-howWorks {
    margin-top: 60px;
    padding-top: 90px;
    background: url(~/assets/images/bg-how-works.png) no-repeat center top;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;

    .how-works-mobile {
        display: none;
    }

    .highlights {
        background: rgb(204, 204, 204);
        background: linear-gradient(90deg, #ebebeb 0%, #ffffff 100%);
        -webkit-border-top-left-radius: 50px;
        -webkit-border-bottom-left-radius: 50px;
        -moz-border-radius-topleft: 50px;
        -moz-border-radius-bottomleft: 50px;
        border-top-left-radius: 50px;
        border-bottom-left-radius: 50px;
    }

    .howWorks-card {
        max-width: 350px;
        margin: 15px auto;
        padding: 8px;

        display: flex;
        align-items: center;

        .icon {
            width: 20%;
            display: inline-block;
            display: flex;
            align-items: center;
        }

        .text {
            width: 80%;
            display: inline-block;

            padding-left: 25px;

            .title {
                font-size: 18px;
                font-weight: 600;
            }

            .content {
                font-size: 16px;
                color: #868c96;
            }
        }
    }

    .howWorksCall-align {
        display: flex;
        align-items: flex-end;
        height: 850px;

        padding: 60px;

        .separator {
            height: 170px;
        }

        .howWorksCall {
            .title {
                font-weight: bold;
                font-size: 45px;
                color: #4293cd;
            }

            .content {
                font-size: 18px;
                color: #868c96;
            }

            .btn-register {
                font-size: 22px;
                font-weight: 600;
                padding: 15px 35px;
            }

            .btn-login {
                font-size: 22px;
                font-weight: 600;
                padding: 15px 35px;
            }

            .actions {}
        }
    }


}

@media (max-width: 900px) {

    .layout-howWorks {
        background: none !important;

        .how-works-mobile {
            display: block;
        }

        .how-works-desktop {
            display: none;
        }

        .howWorksCall-align {
            padding-top: 0;
            height: 300px;
        }

        .actions {
            text-align: center;

            button {
                margin-bottom: 10px;
            }
        }
    }

}
</style>