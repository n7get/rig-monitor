<template>
    <div class="py-3 d-flex justify-content-between w-100 border-bottom">
        <div @click="open_config"><u>Config</u></div>
        <div><b>FT-991A</b></div>
        <div @click="open_mem_chan"><u>Mem chans</u></div>
    </div>

    <div class="mt-2 d-flex">
        <b-button class="col-3" id="op-mode-button" @click="open_op_modes">{{ name }}</b-button>                        
        <frequency class="flex-grow-1" />
    </div>

    <div class="mt-2 d-flex justify-content-between">
        <div><tuner-status /></div>
        <div><lock-status /></div>
        <div><pre-amp-status /></div>
        <div><alc-status /></div>
        <div><mode-status /></div>
        <!-- <manual-mode-status /> -->
    </div>

    <controls />

    <!-- <radio-status class="px-3" /> -->
    <!-- <rbn /> -->

    <groups />
</template>

<script setup>
import { computed } from 'vue';
import { useOpModeStore } from '@/stores/op_modes';
import { useRouter } from 'vue-router';

import frequency from '@/components/frequency.vue';
import controls from '@/components/controls.vue'
import groups from '@/components/groups.vue';
// import radioStatus from '@/components/radio_status.vue'

const router = useRouter();

const name = computed(() => {
    const om_ref = useOpModeStore().get_current_op_mode;
    return om_ref ? om_ref.name : 'Op Mode';
});

const open_op_modes = () => {
    console.log('router: ', router);
    router.push({ name: 'op_modes' });
}

const open_config = () => {
    router.push({ name: 'config' });
}
const open_mem_chan = () => {
    router.push({ name: 'mem_chans' });
}
</script>

<style scoped>
    #op-mode-button {
        height: 64px;
        width: 80px;
    }
</style>
