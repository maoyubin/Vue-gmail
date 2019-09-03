<template>
    <div class="inbox-body">
        <app-messages :messages="trashMessages"></app-messages>
    </div>
</template>

<script>
    import Messages from './Messages.vue';

    export default {
        props:{
            data:{
                type: Object,
                requiresd: true
            }
        },
        computed:{
            trashMessages(){
                return this.data.messages.filter(function(messages){
                        return messages.isDeleted == true;
                });               
            }
        },
        components:{
            appMessages: Messages
        }
    }
</script>