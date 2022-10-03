<template>
    <div id="cil" @click="sender">{{state.mark}}</div>
</template>

<script setup>
import { reactive, defineProps , inject} from 'vue';
const state = reactive({
    mark:'',
    canReplace: true,
})
const prop = defineProps({ activeMark: String ,marker:Number})
const emitter = inject('emitter');

function sender() {
    if (state.canReplace) {
        state.mark = prop.activeMark;
        state.canReplace = false;
        emitter.emit('data__1', prop.marker);
    }
}

emitter.on('end', (e) => {
    state.canReplace = e;
})
emitter.on('clear', () => {
    state.mark = '';
    state.canReplace = true;
})

</script>

<style lang="scss" scoped>
    #cil{
        background-color: lightblue;
        color: #2c3e50;
        font-size: 3.5em;
        font-weight: bold;
        height: 120px;
        line-height: 120px;
        border-radius: 10px;
        cursor: pointer;
    }
</style>