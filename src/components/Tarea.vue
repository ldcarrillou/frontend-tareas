<template>
    <div>
        <h1 class="display-4 text-center">Listado de Tareas</h1>
        <br>
        <div class="row">
            <div class="col-lg-8-offset-lg-2">
                <div class="card mt-4">
                    <div class="card-body">
                        <div class="input-group">
                            <input type="text" v-model="tarea"
                                class="form-control form-control-lg" placeholder="Agregar Tarea">
                            <div class="input-group-append">
                                <button v-on:click="agregarTarea()"
                                    class="btn btn-success btn-lg">Agregar</button>
                            </div>
                        </div>
                        <br />

                        <div class="text-center">
                            <div v-if="loading" class="spinner-border text-success" role="status">
                                <span class="sr-only">Loading...</span>
                            </div>
                        </div>

                        <h5 v-if="listTareas.length == 0">No hay tareas para realizar</h5>
                        
                        <ul v-if="!loading" class="list-group">
                            <li v-for="(tarea, index) of listTareas" :key="index"
                                class="list-group-item d-flex justify-content-between">
                                <!--v-on:click="editarTarea(tarea, index)">-->
                                <span class="cursor" v-bind:class="{'text-success' : tarea.estado}"
                                    v-on:click="editarTarea(tarea, tarea.id)">
                                    <i v-bind:class="[tarea.estado ? 'fas fa-check-circle' : 'far fa-circle']"></i>
                                    <!--<i class="fas fa-check-circle"></i>-->
                                </span>
                                {{ tarea.nombre }}
                                <!--v-on:click="eliminarTarea(index)">-->
                                <span class="text-danger cursor"
                                    v-on:click="eliminarTarea(tarea.id)">
                                    <i class="far fa-trash-alt"></i>
                                </span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
{/*{ listTareas }*/}

<script>
import axios from 'axios';

const URL = "https://backendweb-apptareas20230926173412.azurewebsites.net/api/Tarea/";

    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Tarea',
        data() {
            return {
                tarea: '',
                listTareas: [],
                loading: false
            }
        },
        methods: {
            agregarTarea() {
                const tarea = {
                    nombre: this.tarea,
                    estado: false
                }
                /*this.listTareas.push(tarea);*/
                this.loading = true;
                //axios.post("https://localhost:44311/api/Tarea/", tarea).then(reponse => {
                axios.post(URL, tarea).then(reponse => {
                    console.log(reponse);
                    this.loading = false;
                    this.obtenerTareas();
                }).catch(error => {
                    console.error(error);
                    this.loading = false;
                })
                this.tarea = '';
            },
            //eliminarTarea(index) {
            eliminarTarea(id) {
                /*this.listTareas.splice(index, 1);*/
                this.loading = true;
                //axios.delete("https://localhost:44311/api/Tarea/" + id).then(reponse => {
                axios.delete(URL + id).then(reponse => {
                    console.log(reponse);
                    this.obtenerTareas();
                    this.loading = false;
                }).catch(error => {
                    console.log(error);
                    this.loading = false;
                });
            },
            /*editarTarea(tarea, index) {*/
            editarTarea(tarea, id) {
                /*this.listTareas[index].estado = !tarea.estado*/
                this.loading = true;
                //axios.put("https://localhost:44311/api/Tarea/" + id, tarea).then(() => {
                axios.put(URL + id, tarea).then(() => {
                    this.obtenerTareas();
                    this.loading = false;
                }).catch(() => this.loading = false);
            },
            obtenerTareas() {
                this.loading = true;
                //axios.get("https://localhost:44311/api/Tarea").then(reponse => {
                axios.get(URL).then(reponse => {
                    console.log(reponse);
                    this.listTareas = reponse.data;
                    this.loading = false;
                }).catch(() => this.loading = false);
            }
        },
        created: function() {
            this.obtenerTareas();
        }
    }
</script>

<style scoped>
.cursor {
    cursor: pointer;
}
</style>