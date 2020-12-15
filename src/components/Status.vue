<template>
<div class="row items-center bg-white shadow-16 q-pa-md border">
    <div class="col-8">
        <div class="text-caption">Status</div>
        <div class="text-h4 text-weight-light text-capitalize">
            {{status}}
        <q-icon v-if="status" name="fiber_manual_record" :color="status === 'livre' ? 'positive' : 'negative'" size="18px"/>
        </div>
    </div>
    <div class="col-4 text-right">
        <q-btn v-if="status === 'livre'" @click="$emit('abrirOcupacao')" color="primary" label="Ocupar" :size="tamanhoCustom()" rounded/>
        <q-btn v-if="status !== 'livre'" @click="$emit('desocupar')" color="primary" label="Desocupar" :size="tamanhoCustom()" rounded/>
    </div>
    <div class="text-h6 col-12 text-weight-light" v-if="horarioDesocupacao && status !== 'livre'">
        Pretende desocupar às {{horarioDesocupacao}}
    </div>
</div>
</template>
<script>
export default {
    props: {
        status: {
            type: String
        },
        horarioDesocupacao: {
            type: String
        }
    },
    methods: {
        tamanhoCustom () {
            return this.$q.screen.width < 380 ? '12px' : ''
        }
    }
}
</script>
