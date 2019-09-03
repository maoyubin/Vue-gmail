<template>
    <div class="inbox-body">
        <app-messages :messages="importantMessages"></app-messages>
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
            importantMessages(){
                return this.data.messages.filter(function(messages){
                        return (messages.type == 'incoming' && messages.isImportant && !messages.isDeleted);
                });               
            },
        },
        components:{
            appMessages: Messages
        }
    }
</script>