<template>
    <div>
        <status :status="status" :horarioDesocupacao="'18:40'" @abrirOcupacao="showAgendamento = true" />
        <q-list class="shadow-16 q-mt-lg">
            <q-item>
                <q-item-section>
                    <q-item-label>Henrique</q-item-label>
                </q-item-section>
                <q-item-section side>
                    18:40
                </q-item-section>
            </q-item>
        </q-list>
        <agendamento :mostraDialogAgendar="showAgendamento" ambiente="academia"/>
    </div>
</template>
<script>
import status from 'components/Status'
import agendamento from 'components/Agendamento'
export default {
    data () {
        return {
            status: 'livre',
            showAgendamento: false
        }
    },
    components: { status, agendamento }
}
</script>
