<template>
    <div class="layout-statistics" id="estatisticas">
        <div class="container">
            <div class="row">
                <div class="col-md-4  col-xs-12">
                    <h2>Estatísticas</h2>
                    <div class="card">
                        <div class="content">Mais de 165 mil alunos já passaram por nossas formações. Conheça nossos números atuais, construídos com muito trabalho e parcerias de sucesso pelo país, e venha fazer parte do nosso time vencedor!</div>
                    </div>
                    <div class="effect">
                        <img src="~/assets/images/statistics-bg-effect.jpg" />
                    </div>
                </div>
                <div class="col-md-8  col-xs-12 text-right">
                    <div class="bg-right">
                        <img src="~/assets/images/statistics-bg-right.jpg" v-if="screenShow" />
                    </div>
                    <div class="numbers">
                        <div class="row">
                            <div class="col-md-4  col-xs-12">
                                <h2>450</h2>
                                <span>Instrutores Cadastrados</span>
                            </div>
                            <div class="col-md-4  col-xs-12">
                                <h2>5256</h2>
                                <span>Empresas Atendidas</span>
                            </div>
                            <div class="col-md-4  col-xs-12">
                                <h2>165.158</h2>
                                <span>Alunos Formados</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            screenShow: false
        }
    }
}
</script> 

<style lang="scss" scoped>
.layout-statistics {
    background: url(~/assets/images/statistics-bg-geral.jpg) no-repeat center top;
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
    padding-top: 60px;
    padding-bottom: 100px;

    h2 {
        font-weight: bold;
        font-size: 45px;
        color: #4293cd;
        margin-top: 80px;
        line-height: 100%;
    }

    .card {
        margin-bottom: 30px;

        .content {
            font-size: 18px;
            color: #868c96;
            font-weight: 600;
            line-height: 140%;
        }
    }

    .effect {
        padding-top: 20px;
    }

    .bg-right {
        height: 250px;
    }

    .numbers {
        margin: 0 38px;
        padding-bottom: 20px;
        border-radius: 15px;
        -webkit-box-shadow: 5px 4px 13px -4px #919191;
        box-shadow: 5px 4px 13px -4px #919191;
        text-align: center;
        background: #fff;
        h2 {
            margin: 25px 0;
            font-size: 40px;
            color:#488A47;
        }
        span {
            font-size: 16px;
            font-weight: 600;
        }
    }

    @media (max-width: 900px){
        .bg-right{
            height: 50px;
        }
    }
}
</style>