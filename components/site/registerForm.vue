<template>
    <div class="base-form">
        <div class="content-form">
            <div class="row">
                <div class="col-xs text-left">
                    <h4>Cadastro de Instrutor</h4>
                </div>
                <div class="col-md-1">
                    <h4 @click="registerClose" class="c-pointer">
                        <img src="~/assets/icons/close-modal.png" />
                    </h4>
                </div>
            </div>
            <hr />
            <div class="register-content">
                <div class="row">
                    <div class="col-md-6 col-xs-12">
                        <label class="label">Nome</label>
                        <input class="form-control" type="text" placeholder="Nome" v-model="usName" :class="usNameEmpty == true ? 'empty' : ''" />
                    </div>

                    <div class="col-md-6 col-xs-12">
                        <label class="label">Email</label>
                        <input class="form-control" placeholder="Email" v-model="usEmail" :class="usEmailEmpty == true ? 'empty' : ''" />
                    </div>
                    <div class="col-md-5 col-xs-12">
                        <label class="label">Telefone</label>
                        <input class="form-control" type="text" placeholder="Telefone" v-model="usCelPhone" :class="usCelPhoneEmpty == true ? 'empty' : ''" />
                    </div>

                    <div class="col-md-2  col-xs-6">
                        <label class="label">Estado</label>
                        <select class="form-control" v-model="usState" @change="registerCityList(usState)" :class="usStateEmpty == true ? 'empty' : ''">
                            <option :value="state.stUf" v-for="(state, index) in states" :key="index">
                                {{ state.stUf }}
                            </option>
                        </select>
                    </div>
                    <div class="col-md-5  col-xs-6">
                        <label class="label">Cidade</label>
                        <select class="form-control" v-model="usCity">
                            <option :value="city.ciCity" v-for="(city, index) in citiesList" :key="index">
                                {{ city.ciCity }}
                            </option>
                        </select>
                    </div>
                    <div class="col-md-12  col-xs-12">
                        <label class="label">Selecione os cursos que deseja ministrar</label>

                        <div class="course-list" v-for="(course, indexOptions) in usPreferences" :key="indexOptions">
                            <div class="d-i-block f-left">{{ course.coName }}</div>
                            <div class="d-i-block f-right mobile-delete"><img class="c-pointer" @click="deleteCourse(indexOptions)" src="~/assets/icons/delete.png" width="20" /></div>
                        </div>
                    </div>
                    <div class="col-md-12  col-xs-12 text-center">
                        <button class="btn btn-grey btn-send" @click="registerAddCourse">Incluir Curso</button>
                    </div>
                </div>
            </div>
            <hr />
            <div class="col-md-12" v-if="registerSendConf">
                <div class="alert alert-success">Cadastro efetuado!<br> Aguarde confirmação para iniciar o seu credenciamento.</div>
            </div>

            <div class="col-md-12 text-center" v-else>
                <button class="btn btn-grey btn-send" @click="registerCheckEmptyFields">Enviar Cadastro</button>
            </div>
        </div>
        <div class="select-courses" v-if="showAddCourse">
            <div class="form">
                <div class="row">
                    <div class="col-xs text-left">
                        <h4>Escolha um Curso</h4>
                    </div>
                    <div class="col-md-1">
                        <h4 @click="selectCourseClose" class="c-pointer">
                            <img src="~/assets/icons/close-modal.png" />
                        </h4>
                    </div>
                </div>
                <div class="row">
                    <select class="form-control fs-select" v-model="usPreferencesOptions" @change="selectCourse(usPreferencesOptions)">
                        <option :value="course.id" class="text-center" v-for="(course, index) in coursesList" :key="index" :id="course.id">
                            {{ course.coName }}
                        </option>
                    </select>
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
            homeIsRegister: true,
            showForm: false,
            states: statesJson,
            usState: '',
            usCelPhone: '',
            usEmail: '',
            usCity: '',
            coursesList: '',
            usPreferences: [],
            usPreferencesOptions: [],
            citiesList: [],
            registerSendConf: false,
            showAddCourse: false,
            usNameEmpty: false,
            usCelPhoneEmpty: false,
            usEmailEmpty: false,
            usStateEmpty: false
        }
    },
    mounted() {
        this.registerCourses()
    },
    methods: {
        registerClose() {
            this.$parent.closeModal()
        },
        selectCourseClose() {
            this.showAddCourse = false
        },
        selectCourse(id) {
            var coName = document.getElementById(id).text
            this.usPreferences.push({ id: id, coName: coName })
            this.showAddCourse = false
        },
        registerAddCourse() {
            this.showAddCourse = true
        },

        deleteCourse(index) {
            console.log(index)
            console.log(this.usPreferences)
            this.usPreferences.splice(index, 1)
        },
        async registerCourses() {
            const coursesResult = await $fetch('https://www.institutosc.com.br/api3/courses/getAllToInstructors/1')

            this.coursesList = coursesResult
            this.usPreferencesOptions = coursesResult[0].id
        },
        async registerCheckEmptyFields() {
            var qtdEmpty = 0
            this.usNameEmpty = this.usName == '' ? true : false
            this.usCelPhoneEmpty = this.usCelPhone == '' ? true : false
            this.usEmailEmpty = this.usEmail == '' ? true : false
            this.usStateEmpty = this.usState == '' ? true : false

            if (this.usNameEmpty) qtdEmpty = qtdEmpty + 1
            if (this.usCelPhoneEmpty) qtdEmpty = qtdEmpty + 1
            if (this.usEmailEmpty) qtdEmpty = qtdEmpty + 1
            if (this.usStateEmpty) qtdEmpty = qtdEmpty + 1

            if (qtdEmpty == 0) {
                this.registerButtonDisabled = true
                this.instructorSave()
                setTimeout(() => {
                    this.registerButtonDisabled = false
                }, 1000)
            } else {
                alert('Verifique os campos vazios e tente novamente!')
            }
        },
        async registerCityList(ciUf) {
            const citiesResult = await $fetch('http://localhost:4000/address/getCities/' + ciUf)

            this.citiesList = citiesResult
            this.usCity = citiesResult[0].ciCity
        },
        async instructorSave() {
            var data = {
                usName: this.usName,
                usCelPhone: this.usCelPhone,
                usEmail: this.usEmail,
                usState: this.usState,
                usCity: this.usCity,
                usPreferences : this.usPreferences,
            }
            const list = await $fetch('http://localhost:4000/instructors/create', {
                method: 'POST',
                body: data
            })
            this.registerSendConf = true
        }
    },
    props: ['usName']
}
</script> 


<style lang="scss" scoped>
.base-form {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100vh;
    background: rgba($color: #000000, $alpha: 0.6);
    z-index: 9999999999999;
    text-align: center;
    overflow-y: auto;

    .select-courses {
        position: fixed;
        left: 0;
        top: 0;
        width: 100%;
        height: 100vh;
        background: rgba($color: #000000, $alpha: 0.6);
        z-index: 9999999999999;
        text-align: center;
        overflow-y: auto;
        .form {
            padding: 0 15px 15px 15px;
            width: 95%;
            max-width: 600px;
            background: #fff;
            margin: 200px auto;
            border-radius: 20px;
            overflow: hidden;
            color: #000000;
        }
    }

    .label {
        text-align: left;
        display: block;
    }

    .content-form {
        padding: 0 15px 15px 15px;
        width: 95%;
        max-width: 700px;
        background: #fff;
        margin: 15px auto;
        border-radius: 20px;
        overflow: hidden;
        color: #000000;
        h4 {
            margin-bottom: 5px;
            font-size: 18px;
        }

        .empty {
            border: 1px solid red;
        }

        .register-content {
            background: #fff;

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
            }

            .course-list {
                padding: 10px 5px;
                display: block;
                overflow: hidden;

                &:hover {
                    background: #f3f3f3;
                }
            }
        }

        .btn-send {
            margin-top: 20px;
            padding: 16px 25px;
            font-size: 22px;
            font-weight: 600;
        }
    }

    @media (max-width: 900px){
        .mobile-delete{
            float: none;
            margin: 10px auto;
        }
    }
}
</style>