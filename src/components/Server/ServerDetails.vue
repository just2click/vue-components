<template>
    <div class="col-xs-12 col-sm-6">
        <p v-if="server === null">Server Details are currently not updated</p>
        <section v-if="server !== null">
            <div>Server: {{ server.id }}</div>
            <div>Status: {{ server.status }}</div>
            <div v-if="server && server.status !== 'Normal'">
                <hr>
                <button @click="resetServer">Reset Server</button>
            </div>
        </section>
    </div>

</template>

<script>
    import Server from './Server.vue';
    import { eventBus } from '../../main';

    export default {
        data: function () {
            return {
                server: null
            }
        },
        methods: {
            resetServer () {
                eventBus.$emit('serverWasReset', this.server);
            }
        },
        created () {
            eventBus.$on('serverHasChanged', (server) => {
                this.server = server;
            })
        }
    }
</script>

<style>

</style>
