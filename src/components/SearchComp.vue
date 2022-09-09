<script setup lang="ts">
import { defineProps, defineEmits, PropType, ref} from 'vue';
import { Info } from '../interfaces/interfaces';

const textInputInfo = ref<string>('')
const emit = defineEmits<{
    (e: "addInfo",infoInput: string): void
}>()

function handleAdd() {
    emit('addInfo', textInputInfo.value);
};


</script>

<template>
<form action="">
    <div class="row m-1 p-3">
        <div class="row bg-white rounded shadow-sm p-2 add-todo-wrapper align-items-center justify-content-center">
            <div class="col">
                <input type="text" class="form-control form-control-lg border-0 add-todo-input bg-transparent rounded" placeholder="Add new..." v-model="textInputInfo" />
            </div>
            <div class="col-auto px-0 mx-0 mr-2 flex">
                <i  class="fas fa-calendar-alt mr-3 fs-12 icon-calendar"></i>
                <input type="reset" class="btn btn-primary" value="Add" @click="handleAdd"/>
            </div>  
        </div>
    </div>
</form>
</template>

<style scoped>
.icon-calendar {
    margin-right: 15px;
    color: var(--primary-color);
    font-size: 20px;
    cursor: pointer;
    position: relative;
}
</style>