<template lang="">
    <div>
        <div class="position-absolute mostrar-editar d-flex justify-content-center align-items-center">
            <div class="card position-relative" style="width:400px">
                <div class="close position-absolute bg-danger text-white user-select-none" @click="close">X</div>
                <div class="card-title text-center mt-3">
                    <h3>Asignatura</h3>
                </div>
                <div class="card-body">
                    <h5 class="text-center">
                        {{asignatura.nombre}}
                    </h5>
                    <div>
                        <p>Creditos: {{asignatura.creditos}}</p>
                        <p>Docente: {{getUsuario(asignatura.id_docente)}}</p>
                        <p>Prerrequisito: {{asignatura.prerrequisito == 1 ? "Si" : "No"}}</p>
                        <p>Trabajo Autonomo: {{asignatura.trabajoAutonomo}} horas</p>
                        <p>Trabajo Dirigido: {{asignatura.trabajoDirigido}} horas</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:['asignatura','docentes'],
    created(){
        console.log(this.asignatura)
    },
    methods:{
        close(){
            this.$emitter.emit("close-vista-asignatura")
        },
        getUsuario(id_usuario){
            let indice = this.docentes.findIndex(cate => cate.id== id_usuario)
            if(indice != -1 ) return this.docentes[indice].nombre
            return ""
        }
    }
}
</script>
<style lang="">
    
</style>