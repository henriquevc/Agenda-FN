<template>
<div>
    <q-dialog v-model="mostraDialogAgendar" persistent transition-show="scale" transition-hide="scale">
        <q-card style="min-width: 360px; border-radius: 16px;">
            <q-card-section>
                <div class="text-h6">Agendar</div>
            </q-card-section>

            <q-card-section class="q-gutter-md">
                <q-input v-model="itemAgenda.nome" label="Seu Nome" filled :error="erroNome" @input="erroNome = false"/>
                <div class="row items-center justify-between">
                    <div class="col-12">Horário para agendar</div>
                    <div class="text-h5">{{itemAgenda.horario}}</div>
                </div>
                <!-- <h-time-picker v-model="itemAgenda.horario" /> -->
            </q-card-section>

            <q-card-actions align="right" class="bg-white text-teal">
                <q-btn @click="fechar" flat rounded label="cancelar" color="primary" />
                <q-btn @click="agendar" label="Ok" rounded color="primary"/>
            </q-card-actions>
        </q-card>
    </q-dialog>
</div>
</template>
<script>
export default {
    props: {
        mostraDialogAgendar: {
            type: Boolean,
            default: false
        },
        horarioDesocupacao: {
            type: String
        },
        ambiente: {
            type: String
        }
    },
    data () {
        return {
            itemAgenda: {},
            erroNome: false,
            exibirModal: false
        }
    },
    mounted () {
        if (this.itemAgenda.Nome || this.itemAgenda.horario) {
            this.itemAgenda = {}
        }
    },
    methods: {
        agendar () {
            return this.$q.screen.width < 380 ? '12px' : ''
        },
        fechar () {
            this.$emit('input', 'mostraDialogAgendar', false)
        }
    }
}
</script>
