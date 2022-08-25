<template>
    <div class="layout-about-us" id="sobre-nos">
        <div class="container">
            <div class="row">
                <div class="col-md-6 col-xs-12">
                    <h2>Sobre Nós</h2>
                    <div class="card">
                        <div class="title">Missão</div>
                        <div class="content">Auxiliar pessoas e empresas a realizarem com excelência os treinamentos em Segurança do Trabalho de forma simples e rápida, mantendo sempre a qualidade que o tema exige.</div>
                    </div>
                    <div class="card">
                        <div class="title">Visão</div>
                        <div class="content">Ser a empresa número um do Brasil em nível técnico e em abrangência territorial nos treinamentos de Segurança do Trabalho.</div>
                    </div>
                    <div class="card">
                        <div class="title">Valores </div>
                        <div class="content">Transparência, honestidade, conhecimento técnico, valorização e respeito à vida, crescimento sustentável, empreendedorismo e inovação tecnológica.</div>
                    </div>
                </div>
                <div class="col-md-6  col-xs-12 text-right">
                    <img src="~/assets/images/empty-video.jpg" />
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.layout-about-us {
    padding-top:120px;   
    margin-top: 60px;
    margin-bottom: 45px;

    h2 {
        font-weight: bold;
        font-size: 45px;
        color: #4293cd;       
        margin-top:0;
        line-height: 100%;
    }

    .card {
        margin-bottom: 30px;
        .title {
            font-size: 22px;
            color: #488A47;
            font-weight: 700;
            line-height: 140%;
        }

        .content {
            font-size: 18px;
            color: #868C96;
            font-weight: 600;
            line-height: 140%;
        }
    }
}
</style>