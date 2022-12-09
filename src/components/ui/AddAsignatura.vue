<template lang="">
    <div>
        <div class="position-absolute mostrar-editar d-flex justify-content-center align-items-center">
            <div class="card position-relative" style="width:400px">
                <div class="close position-absolute bg-danger text-white user-select-none" @click="close">X</div>
                <div class="card-title text-center mt-3">
                    <h3>Crear Asignatura</h3>
                </div>
                <form @submit.prevent="crearPost" class="container mb-4">
                    <input type="text" required placeholder="Nombre" v-model="nombre" class="form-control m-1" >
                    <input type="number" required placeholder="Creditos" v-model="creditos" class="form-control m-1" />
                    <input type="number" required placeholder="Prerrequisito" v-model="prerrequisito" class="form-control m-1" />
                    <input type="number" required placeholder="Trabajo Autonomo" v-model="trabajoAutonomo" class="form-control m-1" />
                    <input type="number" required placeholder="Trabajo Dirigido" v-model="trabajoDirigido" class="form-control m-1" />

                    <select class="form-select m-1" aria-label="Default select example"  required  v-model="id_docente">
                        <option disabled value="">Seleccionar Docente</option>
                        <option v-for="categoria in docentes" :value="categoria.id">{{categoria.nombre}}</option>
                    </select>
                    <div class="d-flex mt-3">
                        <button class="btn btn-primary m-1 m-auto">Crear</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:['categorias','docentes'],
    data(){
        return{
            nombre:"",
            creditos: "",
            id_docente: "",
            prerrequisito: "",
            trabajoAutonomo:"",
            trabajoDirigido:""
        }
    },
    created(){
    },
    methods:{
        close(){
            this.$emitter.emit("close-add-post")
        },
        crearPost(){
            let informacion = {
                nombre:this.nombre,
                creditos: this.creditos,
                id_docente: this.id_docente,
                prerrequisito: this.prerrequisito,
                trabajoAutonomo:this.trabajoAutonomo,
                trabajoDirigido:this.trabajoDirigido
            }
            this.axios.post(this.$path() + "/asignatura/", informacion,this.$header())
                .then(resp => {
                    this.$emitter.emit("crear-post", informacion)
                })
        }
    }
}
</script>
<style lang="">
    
</style>