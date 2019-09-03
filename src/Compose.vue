<template>
<div>
    <a href="#composeModal" data-toggle="modal" class="btn btn-compose">Compose</a>

    <div tabindex="-1" role="dialog"  id="composeModal" class="modal fade" style="display: none;">
                <div class="modal-dialog" role="document">
                    <div class="modal-content">
                            <div class="modal-header">
                                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                <span aria-hidden="true">&times;</span>
                                </button>
                                <h5 class="modal-title">New Message</h5>
                            </div>
                            <div class="modal-body">
                                <form role="form" class="form-horizontal" @submit.prevent="sendMessage">
                                <div class="form-group">
                                    <label for="subject" class="col-lg-2 control-labe">Subject</label>
                                    <div class="col-lg-10">
                                        <input type="text" id="subject" class="form-control" v-model="message.subject">
                                    </div>
                                </div>

                                <div class="form-group">
                                    <label for="message" class="col-lg-2 control-labe">Message</label>
                                    <div class="col-lg-10">
                                        <textarea rows="10" clos="30" id="message" class="form-control" v-model="message.content"></textarea>
                                    </div>
                                </div>

                                <div class="form-group">
                                    <div class="col-lg-offset-2 col-lg-10">
                                        <button class="btn btn-send" type="submit">Send</button>
                                    </div>
                                </div>
                            </form>
                            </div>
                    </div>
                </div>
    </div>
</div>
</template>

<script>
import { eventBus } from './main';
import moment from 'moment';

export default {
    data() {
        return {
            message:{
                subject: '',
                content:''
            }
        }
    },
    methods: {
        sendMessage(){
            eventBus.$emit('sentMessage', {
                message: {
                    subject: this.message.subject,
                    content: this.message.content,
                    isDeleted: false,
                    type: 'outgoing',
                    date: moment(),
                    from: {
                        name: 'Matt mby',
                        email: 'xxxxx@asdfas.com'
                    },
                    attachments: []
                }
            });
        }
    }
}
</script>
