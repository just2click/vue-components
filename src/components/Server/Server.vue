<template>
    <div>
        <li class="list-group-item" @click="openServerDetails">
            Server #{{ server.id }}
        </li>
    </div>

</template>

<script>
import { eventBus } from '../../main.js';

export default {

    props: ['server'],
    methods: {
        openServerDetails () {
            eventBus.$emit('serverHasChanged', this.server)
        }
    }
}
</script>
