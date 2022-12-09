<template lang="">
    <div v-if="isLogin">
        <nav-bar></nav-bar>
        <div class="container">
            <h1 class="text-center mt-5">Asignatura</h1>
        </div>
        <div class="container">
            <hr/>
        </div>
        <div class="container d-flex justify-content-center flex-wrap">
            <div class="card m-1" v-for="asignatura, indice in asignaturas"  style="width:350px">
                <div class="card-body">
                    <div class="card-title mt-3 d-flex align-items-center">
                        <h4 style="margin-bottom:0px">{{asignatura.nombre}}</h4>
                    </div>
                    <div class="card-title mt-3">
                        <h6>Creditos: {{asignatura.creditos}}</h6>
                    </div>
                    <div class="d-flex align-items-center">
                        <div>
                            Docente:
                        </div>
                        <div class="alert-perso">
                            {{getUsuario(asignatura.id_docente)}}
                        </div>
                    </div>
                    <div class="d-flex mt-3">
                        <button class="btn btn-primary m-1 m-auto" v-if="rolUserLog=='COORD'" @click="editar(indice)">Editar</button>
                        <button class="btn btn-success m-1 m-auto" @click="publicar(indice)">Ver</button>
                        <button class="btn btn-danger m-1 m-auto"  v-if="'COORD' == rolUserLog"  @click="eliminar(indice)">Eliminar</button>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="rolUserLog == 'COORD'" class="btn btn-primary btn-max-circle" @click="open">
            +
        </div>
        <add-asignatura v-if="newPost" :docentes="usuarios"/>
        <edit-asignatura v-if="informacionEditar != null" :docentes="usuarios" :asignatura="informacionEditar"/>
        <ver-asignatura v-if="ver != null" :docentes="usuarios" :asignatura="ver"/>
        <div v-if="isEliminar != -1" class="position-absolute mostrar-editar d-flex justify-content-center align-items-center">
            <div class="card position-relative" style="width:350px">
                <div class="card-title text-center mt-3">
                    <h3>Mensaje</h3>
                    <p>
                        ¿Esta seguro que desea eliminar el usuario?
                    </p>
                    <div>
                        <button class="btn btn-danger m-1" @click="eliminar">
                            Aceptar
                        </button>
                        <button class="btn btn-primary m-1" @click="cancelar">
                            Cancelar
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import NavBar from '../ui/NavBar.vue'
import AddAsignatura from '../ui/AddAsignatura.vue'
import EditAsignatura from '../ui/EditAsignatura.vue'
import VerAsignatura from '../ui/VerAsignatura.vue'
export default {
    name: "Home",
    components: {
        NavBar,
        AddAsignatura,
        EditAsignatura,
        VerAsignatura
    },
    data() {
        return {
            isEliminar:-1,
            isLogin: false,
            newPost:false,
            usuarios:[],
            asignaturas:[],
            rolUserLog:null,
            idUserLog:null,
            informacionEditar:null,
            ver:null
        }
    },
    created(){
        this.rolUserLog = sessionStorage.getItem("rol")
        this.idUserLog = sessionStorage.getItem("usuario")
    },
    mounted() {
        if (!this.$isRegistre()) {
            this.$router.push('/login')
        } else {
            this.isLogin = true
            this.traerUsuarios()
            this.traerAsignaturas()
        }
        this.$emitter.on("close-add-post", ()=> {
            this.newPost=false
            this.informacionEditar=null
        })
        this.$emitter.on("crear-post", ()=> {
            this.traerAsignaturas()
            this.newPost=false
            this.informacionEditar=null
        })
        this.$emitter.on("close-vista-asignatura", ()=> this.ver=null)
    },
    methods: {
        traerUsuarios() {
            this.axios.get(this.$path() + "/docente", this.$header())
                .then(resp => {
                    this.usuarios=resp.data
                })
        },
        traerAsignaturas(){
            this.axios.get(this.$path() + "/asignatura/", this.$header())
                .then(resp => {
                    console.log(resp.data)
                    this.asignaturas=resp.data
                })
        },
        getUsuario(id_usuario){
            let indice = this.usuarios.findIndex(cate => cate.id== id_usuario)
            if(indice != -1 ) return this.usuarios[indice].nombre
            return ""
        },
        open(){
            this.newPost=true
        },
        cancelar(){
            this.isEliminar=-1
        },
        eliminar(indice){
            if(this.isEliminar == -1){
                this.isEliminar=indice
            }else{
                
                this.axios.delete(this.$path() + "/asignatura/"+this.asignaturas[this.isEliminar].id, this.$header())
                .then(resp => {
                    this.traerAsignaturas()
                    this.isEliminar=-1
                })
            }
        },
        publicar(indice){
            this.ver=this.asignaturas[indice]
        },
        editar(indice){
            this.informacionEditar = this.asignaturas[indice]
        }
    },
}
</script>
<style lang="">
    
</style>