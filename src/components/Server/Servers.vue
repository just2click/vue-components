<template>
    <div class="col-xs-12 col-sm-6">
        <ul class="list-group">
            <server-component :key="index" v-for="index in servers.length" :server="servers[index - 1]"></server-component>
        </ul>
    </div>
</template>

<script>
    import Server from './Server.vue';
    import { eventBus } from '../../main.js'

    export default {
        components: {
            'server-component': Server
        },
        data: function () {
            return {
                servers: [
                    { id: 1, status: 'Normal' },
                    { id: 2, status: 'Critical' },
                    { id: 3, status: 'Warning' },
                    { id: 4, status: 'Idle' }
                ]
            }
        },
        created () {
            eventBus.$on('serverWasReset', (serverToReset) => {
                const selectedServer = this.servers.filter(server => {
                    return serverToReset.id === server.id
                });

                if (selectedServer.length) {
                    selectedServer[0].status = 'Normal';
                }
            });
        }
    }
</script>

<style>

</style>
