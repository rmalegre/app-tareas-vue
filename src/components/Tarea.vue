<template>
    <div>
        <h1 class="display-4 text-center mt-2">Listado de Tareas</h1>
        <hr />
        <div class="col-lg-8 offset-lg-2">
            <div class="card mt-4">
                <div class="card-body">
                    <div class="input-group">
                        <input type="text" v-model="tarea" class="form-control form-control-lg"
                            placeholder="Agregar Tarea" />
                        <div class="input-group-append">
                            <button v-on:click="agregarTarea()" class="btn btn-success btn-lg">Agregar</button>
                        </div>
                    </div>

                    <br />
                    <h5 v-if="listTareas.length == 0">No hay tareas para realizar</h5>

                    <ul class="list-group ">
                        <li v-for="(tarea, index) of listTareas" :key="index"
                            class="list-group-item d-flex justify-content-between">
                            <span class="cursor" v-bind:class="{ 'text-success': tarea.estado }"
                                v-on:click="editarTarea(tarea, index)">
                                <i v-bind:class="[tarea.estado ? 'fa-solid fa-circle-check' : 'far fa-circle']"></i>
                            </span>
                            {{ tarea.nombre }}
                            <span class="text-danger cursor " v-on:click="eliminarTarea(index)">
                                <i class="fas fa-trash-alt"></i>
                            </span>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: 'Tarea',
    data() {
        return {
            tarea: '',
            listTareas: []
        }
    },
    methods: {
        agregarTarea() {
            const tarea = {
                nombre: this.tarea,
                estado: false
            }
            this.listTareas.push(tarea);
            this.tarea = ''
        },
        eliminarTarea(index) {
            this.listTareas.splice(index, 1);
            console.log(this.listTareas)
        },
        editarTarea(tarea, index) {
            this.listTareas[index].estado = !tarea.estado
        }
    }

}
</script>

<style scoped>
.cursor {
    cursor: pointer;
}
</style>
