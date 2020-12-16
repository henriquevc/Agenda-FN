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
                    <div class="col-12">Selecione os dias para agendar</div>
                    <q-chip v-for="dia in dias" :key="dia" :color="diasSelecionados.includes(dia) ? 'teal' : ''" :text-color="diasSelecionados.includes(dia) ? 'white' : 'grey-9'" @click="toggleDia(dia)" clickable>
                        {{dia}}
                    </q-chip>
                </div>
                <div class="row items-center justify-between">
                    <div class="col-12">Horário para agendar</div>
                    <q-chip v-for="horario in horarios" :key="horario" :color="horariosSelecionados.includes(horario) ? 'teal' : ''" :text-color="horariosSelecionados.includes(horario) ? 'white' : 'grey-9'" @click="toggleHorario(horario)" clickable>
                        {{horario}}
                    </q-chip>
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
            exibirModal: false,
            dias: ['Seg', 'Ter', 'Qua', 'Qui', 'Sex', 'Sab', 'Dom'],
            diasSelecionados: [],
            horarios: ['06:00 - 07:00', '07:00 - 08:00'],
            horariosSelecionados: []
        }
    },
    mounted () {
        if (this.itemAgenda.Nome || this.itemAgenda.horario) {
            this.itemAgenda = {}
        }
    },
    methods: {
        toggleDia (dia) {
            if (this.diasSelecionados.includes(dia)) {
                this.diasSelecionados.splice(this.diasSelecionados.indexOf(dia), 1)
            } else {
                this.diasSelecionados.push(dia)
            }
        },
        toggleHorario (horario) {
            if (this.horariosSelecionados.includes(horario)) {
                this.horariosSelecionados.splice(this.horariosSelecionados.indexOf(horario), 1)
            } else {
                this.horariosSelecionados.push(horario)
            }
        },
        agendar () {
            this.$emit('agendar', this.itemAgenda)
        },
        fechar () {
            this.$emit('update:mostraDialogAgendar', false)
        }
    }
}
</script>
