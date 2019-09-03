<template>
    <aside class="sm-side">
         <div class="user-head">
            <img src="src/assets/images/profile.jpg">
            <div class="user-name">
                <h5>Matt</h5>
                <span class="email-address">xxx@asfsa.com</span>
            </div>
        </div>

        <div class="compose-wrapper">
            <app-compose></app-compose>
        </div>

        <ul class="inbox-nav">
            <li >
                <a href="#" @click.prevent="navigate('app-inbox','Inbox')">
                    <i class="fa fa-inbox"></i>Inbox <span class="label label-danger pull-right">{{ unreadMessages.length }}</span>
                </a>
            </li>
            <li>
                <a href="#" @click.prevent="navigate('app-sent','Sent')">
                    <i class="fa fa-envelope-o"></i>Sent <span class="label label-default pull-right">{{ sendMessages.length }}</span>
                </a>
            </li>
            <li>
                <a href="#" @click.prevent="navigate('app-important','Important')">
                    <i class="fa fa-bookmark-o"></i>Important <span class="label label-warning pull-right">{{ importantMessages.length }}</span>
                </a>
            </li>
            <li>
                <a href="#" @click.prevent="navigate('app-trash','Trash')">
                    <i class="fa fa-trash-o"></i>Trash <span class="label label-default pull-right">{{ trashMessages.length }}</span>
                </a>
            </li>
        </ul>
    </aside>
</template>

<script>
    import {eventBus} from './main';
    import messages from './data/messages';
    import Compose from './Compose.vue';

    export default {
        props:{
            messages:{
                type: Array,
                requiresd: true
            }
        },
        methods:{
            navigate(newView,title){
                eventBus.$emit('changeView',{
                    tag:newView,
                    title:title
                });
            }
        },
        computed:{
            unreadMessages(){
                return this.messages.filter(function(messages){
                        return (messages.type == 'incoming' && !messages.isRead && !messages.isDeleted);
                });               
            },
            sendMessages(){
                return this.messages.filter(function(messages){
                        return (messages.type == 'outgoing' && !messages.isDeleted);
                });               
            },
            importantMessages(){
                return this.messages.filter(function(messages){
                        return (messages.type == 'incoming' && messages.isImportant && !messages.isDeleted);
                });               
            },
            trashMessages(){
                return this.messages.filter(function(messages){
                        return messages.isDeleted == true;
                });               
            },
        },
        components: {
            appCompose: Compose
        }
    }
</script>