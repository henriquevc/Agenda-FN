<template>
    <div>
        <status :status="status" :horarioDesocupacao="'18:40'" @abrirOcupacao="showAgendamento = true" />
        <q-list class="q-mt-md">
            <q-item v-for="item in lista" :key="item.key" class="q-mt-md shadow-16 border-rounded">
                <q-item-section>
                    <q-item-label class="text-weight-bold">{{item.nomeUsuario}}</q-item-label>
                    <q-item-label caption>{{item.horarioInicial}} - {{item.horarioFinal}} </q-item-label>
                </q-item-section>
                <q-item-section side>
                    <q-btn icon="delete" size="14px" flat round color="negative" @click="excluirItemAgenda(item.key)">
                        <q-tooltip>remover</q-tooltip>
                    </q-btn>
                </q-item-section>
            </q-item>
        </q-list>
        <agendamento :mostraDialogAgendar.sync="showAgendamento" @agendar="agendar" />
    </div>
</template>
<script>
import status from 'components/Status'
import agendamento from 'components/Agendamento'

import firebase from 'firebase/app'
import 'firebase/database'
export default {
    data () {
        return {
            status: 'livre',
            showAgendamento: false,
            lista: [],
            ambiente: null
        }
    },
    components: { status, agendamento },
    created () {
        const firebaseConfig = {
            apiKey: 'AIzaSyD_KYtOyBbwy8Cpk_iFZ4wEoGlYnctNwpE',
            authDomain: 'agenda-fn.firebaseapp.com',
            databaseURL: 'https://agenda-fn-default-rtdb.firebaseio.com',
            projectId: 'agenda-fn',
            storageBucket: 'agenda-fn.appspot.com',
            messagingSenderId: '906361868116',
            appId: '1:906361868116:web:1c8b7dcc6368cba88242c1',
            measurementId: 'G-1HQ8431XYB'
        }

        firebase.initializeApp(firebaseConfig)
        this.ambiente = this.$route.params.nomeAmbiente
        this.montarListagem(this.ambiente)
    },
    watch: {
        '$route' (to) {
            this.ambiente = to.params.nomeAmbiente
            this.montarListagem(this.ambiente)
        }
    },
    methods: {
        montarListagem (ambiente) {
            firebase.database().ref(`agenda/${ambiente}`).on('value', snapshot => {
                this.lista = []
                const valores = snapshot.val()
                for (const prop in valores) {
                    this.lista.push({
                        key: prop,
                        nomeUsuario: valores[prop].nomeUsuario,
                        horarioInicial: valores[prop].horarioInicial,
                        horarioFinal: valores[prop].horarioFinal
                    })
                    this.lista.sort((a, b) => {
                        if (a.horario > b.horario) {
                            return 1
                        }
                        if (b.horario > a.horario) {
                            return -1
                        }
                        return 0
                    })
                }
            })
        },
        agendar (obj) {
            const key = firebase.database().ref().child('agenda/academia').push().key
            firebase.database().ref(`agenda/academia/${key}`).set(obj)
        },
        excluirItemAgenda (chave) {
            firebase.database().ref(`agenda/${this.ambiente}/${chave}`).remove()
        }
    }
}
</script>
<style>
    .border-rounded {
        border-radius: 10px;
    }
</style>
