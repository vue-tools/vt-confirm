<style src="./style.css"></style>
<script>
    import Vue from 'vue'
    import plugin from './plugin'

    let Component = {
        props: {
            visible: {
                type: Boolean,
                required: true
            }
        },
        data() {
            return {
                cancelAccess: false,
                confirmAccess: false
            }
        },
        render(h) {
            return (
                <transition name="ui-confirm-fade">
                    <div class="ui-confirm" v-show={this.visible}>
                        <transition name="ui-confirm-zoomOut">
                            <div class="ui-confirm__container" v-show={this.visible}>
                                <p class="ui-confirm__title">{this.$slots.title}</p>
                                <p class="ui-confirm__info">{this.$slots.text}</p>
                                <div class="ui-confirm__button">
                                    <div class={{"ui-confirm__button--ok": true, "ui-confirm-button--access": this.confirmAccess}} onClick={this.emit.bind(this, true)} onTouchstart={this.confirmHandle.bind(this, 0)} touchend={this.confirmHandle.bind(this, 200)}>
                                        {this.$slots.confirmButton || '确定'}
                                    </div>
                                    <div class={{"ui-confirm__button--cancel": true, "ui-confirm-button--access": this.cancelAccess}} onClick={this.emit.bind(this, false)} onTouchstart={this.cancelHandle.bind(this, 0)} touchend={this.cancelHandle.bind(this, 200)}>
                                        {this.$slots.cancelButton || '取消'}
                                    </div>
                                </div>
                            </div>
                        </transition>
                    </div>
                </transition>
            )
        },
        methods: {
            emit(bool) {
                this.$emit('hide', bool)
            },
            confirmHandle(time) {
                setTimeout(() => {
                    this.confirmAccess = !this.confirmAccess
                }, time)
            },
            cancelHandle(time) {
                setTimeout(() => {
                    this.cancelAccess = !this.cancelAccess
                }, time)
            }
        }
    }

    Vue.use(plugin, Component)
    
    export default Component
</script>