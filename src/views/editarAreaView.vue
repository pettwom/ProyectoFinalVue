<template>
    <div class="home">
        <br>
        <br>

        <div class="mdl-tabs__panel is-active" id="gestionArea">
            <div class="mdl-grid">
                <div
                    class="mdl-cell mdl-cell--4-col-phone mdl-cell--8-col-tablet mdl-cell--8-col-desktop mdl-cell--2-offset-desktop">
                    <div class="full-width panel mdl-shadow--2dp">
                        <div class="full-width panel-tittle bg-primary text-center tittles">
                            Editar Áreas de Trabajo
                        </div>
                        <div class="full-width panel-content">
                            <form @submit.prevent="guardar()">
                                <h5 class="text-condensedLight">Información Básica</h5>
                                <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
                                    <input class="mdl-textfield__input" type="text "
                                        pattern="-?[A-Za-z0-9áéíóúÁÉÍÓÚ ]*(\.[0-9]+)?" id="area" name="area"
                                        v-model="areas.nombre">
                                    <label class="mdl-textfield__label" for="area">Área de Trabajo</label>
                                    <span class="mdl-textfield__error">Dato inválido</span>
                                </div>
                                <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
                                    <input class="mdl-textfield__input" type="text "
                                        pattern="-?[A-Za-z0-9áéíóúÁÉÍÓÚ ]*(\.[0-9]+)?" id="encargado" name="encargado"
                                        v-model="areas.encargado">
                                    <label class="mdl-textfield__label" for="encargado">Encargado</label>
                                    <span class="mdl-textfield__error">Dato Inválido</span>
                                </div>
                                <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
                                    <input class="mdl-textfield__input" type="number " pattern="-?[0-9]*(\.[0-9]+)?"
                                        id="cantidad" name="cantidad" v-model="areas.cantidad">
                                    <label class="mdl-textfield__label" for="cantidad">Cantidad de
                                        dependientes</label>
                                    <span class="mdl-textfield__error">Dato Inválido</span>
                                </div>
                                <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label">
                                    <div class="switch">
                                        <label class="mdl-textfield__label" for="estadoArea">Estado</label>
                                        <label>
                                            No
                                            <input type="checkbox" name="estado" id="estadoArea" v-model="areas.estado">
                                            <span class="lever"></span>
                                            Si
                                        </label>
                                    </div>
                                </div>

                                <p class="text-center">
                                    <button
                                        class="mdl-button mdl-js-button mdl-button--fab mdl-js-ripple-effect mdl-button--colored bg-primary"
                                        id="btn-addPayment">
                                        <i class="zmdi zmdi-plus"></i>
                                    </button>
                                <div class="mdl-tooltip" for="btn-addPayment">Modificar Área</div>
                                </p>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>
<script>
import { assertExpressionStatement } from '@babel/types';

export default {
    name: 'area',
    data() {
        return {
            areas: {
                nombre: '',
                encargado: '',
                cantidad: null,
                estado: []
            }
        }
    },
    methods: {
        guardar() {
            axios({
                method: 'PATCH',
                url: 'http://localhost:3000/Area/' + this.$route.params.id,
                data: this.areas
            })
                .then(response => {
                    this.$router.push('/area');
                })
        },
        getArea() {
            axios({
                method: 'GET',
                url: 'http://localhost:3000/Area/' + this.$route.params.id,
            })
                .then(response => {
                    this.areas = response.data
                })
        },

    },
    mounted() {
        this.getArea()
    }
}
</script>
