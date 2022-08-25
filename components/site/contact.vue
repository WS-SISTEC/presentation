<template>
    <div class="layout-contact" id="contato">
        <div class="row">
            <div class="col-md-6  ">
                <!--https://maps.google.com/maps?hl=en&amp;q=Rua+Manoel+Joaquim+Coelho+249%2C+sala+02%2C+Dom+Bosco Itajai - SC&amp;ie=UTF8&amp;t=&amp;z=13&amp;iwloc=B&amp;output=embed
                <iframe width="100%" height="650" id="mapEs" src="https://maps.google.com/maps?hl=en&amp;q=Rua+Manoel+Joaquim+Coelho+249%2C+sala+02%2C+Dom+Bosco Itajai - SC&amp;ie=UTF8&amp;t=&amp;z=13&amp;iwloc=B&amp;output=embed" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"></iframe>-->
                <img src="~/assets/images/map-localization.png" />

            </div>
            <div class="col-md-6 col-xs-12 zindex">
                <div class="form">
                    <div class="title">Contato</div>
                    <div class="content">Para dúvidas, sugestões ou reclamações, entre em contato conosco pelo nosso email. Nossa equipe prontamente responderá à sua mensagem!</div>
                    <div class="home-text-contact">
                        <div class="contact-content">
                            <div class="row">
                                <div class="col-md-6 col-xs-12">
                                    <label class="label">Nome</label>
                                    <input class="form-control" type="text" placeholder="Nome" v-model="coName" :class="coNameEmpty == true ? 'empty' : ''"/>
                                </div>

                                <div class="col-md-6 col-xs-12">
                                    <label class="label">Email</label>
                                    <input class="form-control" placeholder="Email" v-model="coEmail" :class="coEmailEmpty == true ? 'empty' : ''" />
                                </div>
                                <div class="col-md-5 col-xs-12">
                                    <label class="label">Telefone</label>
                                    <input class="form-control" type="text" placeholder="Telefone" v-model="coPhone" :class="coPhoneEmpty == true ? 'empty' : ''" />
                                </div>

                                <div class="col-md-2 col-xs-6">
                                    <label class="label">Estado</label>
                                    <select class="form-control" v-model="coState" @change="contactsCityList(coState)" :class="coStateEmpty == true ? 'empty' : ''">
                                        <option class="text-center" v-for="(state, index) in states" :key="index">
                                            {{ state.stUf }}
                                        </option>
                                    </select>
                                </div>
                                <div class="col-md-5 col-xs-6">
                                    <label class="label">Cidade</label>
                                    <select class="form-control" v-model="coCity">
                                        <option :value="city.ciCity" v-for="(city, index) in citiesList" :key="index">
                                            {{ city.ciCity }}
                                        </option>
                                    </select>
                                </div>
                                <div class="col-md-12 col-xs-12">
                                    <label class="label">Mensagem</label>
                                    <textarea class="form-control" name="form" id="form" v-model="coContent" cols="65"
                                        rows="4" placeholder="Digite sua mensagem aqui" :class="coContentEmpty == true ? 'empty' : ''">
                                    </textarea>
                                </div>
                                <div class="col-md-12 col-xs-12" v-if="contactSendConf">
                                    <div class="alert alert-success">Mensagem enviada, logo entraremos em contato!</div>
                                </div>
                                <div class="col-md-12 col-xs-12 text-center" v-else>
                                    <button :disabled="contactButtonDisabled" class="btn btn-grey btn-send" @click="contactCheckEmptyFields">Enviar</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>



<script>
import statesJson from '~/public/states.json'
export default {
    data() {
        return {
            screenShow: false,
            posts: {},
            states: statesJson,
            contactSendConf: false,
            coState: '',
            coCity: '',
            coName: '',
            coPhone: '',
            coEmail: '',
            coCity: '',
            citiesList: [],
            coContent: '',            
            coNameEmpty: false,
            coPhoneEmpty: false,
            coEmailEmpty: false,
            coStateEmpty: false,
            coContentEmpty: false,
            contactButtonDisabled: false
        }
    },

    methods: {
        async contactSend() {
            var data = {
                coName: this.coName,
                coPhone: this.coPhone,
                coEmail: this.coEmail,
                coState: this.coState,
                coCity: this.coCity,
                coContent: this.coContent
            }
            const list = await $fetch('http://localhost:4000/contacts/create', {
                method: 'POST',
                body: data
            })
            this.contactSendConf = true
        },
        
        async contactCheckEmptyFields() {
            var qtdEmpty = 0
            this.coNameEmpty = this.coName == '' ? true : false
            this.coPhoneEmpty = this.coPhone == '' ? true : false
            this.coEmailEmpty = this.coEmail == '' ? true : false
            this.coStateEmpty = this.coState == '' ? true : false
            this.coContentEmpty = this.coContent == '' ? true : false

            if (this.coNameEmpty) qtdEmpty = qtdEmpty + 1
            if (this.coPhoneEmpty) qtdEmpty = qtdEmpty + 1
            if (this.coEmailEmpty) qtdEmpty = qtdEmpty + 1
            if (this.coStateEmpty) qtdEmpty = qtdEmpty + 1
            if (this.coContentEmpty) qtdEmpty = qtdEmpty + 1

            if (qtdEmpty == 0) {
                this.contactButtonDisabled = true
                this.contactSend()
                setTimeout(() => {
                    this.contactButtonDisabled = false
                }, 1000)
            } else {
                alert('Verifique os campos vazios e tente novamente!')
            }
        },
        async contactsCityList(ciUf) {
            const citiesResult = await $fetch('http://localhost:4000/address/getCities/' + ciUf)

            this.citiesList = citiesResult
            this.coCity = citiesResult[0].ciCity
        },
    }
}
</script> 

<style lang="scss" scoped>
.layout-contact {
    padding-top: 120px;

    .pd-contact {
        padding-left: 0;
        padding-right: 0;
        position: relative;
        overflow: hidden;
        margin-right: -80px;
        z-index: 10;
    }

    .zindex {
        z-index: 99;
    }

    .form {
        z-index: 999999;

        .title {
            font-weight: bold;
            font-size: 45px;
            color: #4293cd;
        }

        .content {
            font-size: 18px;
            color: #868c96;
        }

        .separator {
            height: 170px;
        }
    }

    .cut {
        background: #fff;
        /* A cor dos elementos antes e depois */
        display: block;
        top: 0;
        bottom: 0;
        position: absolute;
        width: 200px;
    }

    .right {
        -webkit-transform: skew(16deg) translateX(70px);
        -ms-transform: skew(16deg) translateX(70px);
        transform: skew(16deg) translateX(70px);
        right: -25px;
    }

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

    .home-text-contact {
        margin-top: 10px;

        

        .contact-content {
            border-radius: 15px;
            -webkit-box-shadow: 5px 4px 13px -4px #919191;
            box-shadow: 5px 4px 13px -4px #919191;
            background: #fff;
            color: #000;
            margin: 45px 0;
            padding: 20px;

            .btn-send {
                margin-top: 20px;
                padding: 16px 25px;
                font-size: 22px;
                font-weight: 600;
            }

            .empty{
                border:1px solid red;
            }

            .form-control {
                padding-left: 1px;
                color: #868c96 !important;
                font-size: 18px;

                &::placeholder {
                    /* Chrome, Firefox, Opera, Safari 10.1+ */
                    color: #868c96;
                    opacity: 1;
                    /* Firefox */
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
            }
        }
    }
}
</style>