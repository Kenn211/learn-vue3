<script setup lang="ts">
import { defineProps, defineEmits, PropType } from 'vue';
import { Info } from '../interfaces/interfaces';


const props = defineProps <{
    info: Info
}>()

const emit = defineEmits<{
    (e: 'deleteInfo', data: Info): void
    (e: 'toActive', data: Info, status: string): void
    (e: 'toCompleted', data: Info,status: string): void
    (e: 'toHasDueDate', data: Info,status: string): void
    // (e: 'handleChangeStatus', data: Info,status: string): void
}>()


function handleDelete(): void {
    var data= {
        id: props.info.id,
        title: props.info.title,
        status: props.info.status
    }
    emit('deleteInfo', data);
};

// function handleChangeStatus(): void {
//     var data = {
//         id: props.info.id,
//         title: props.info.title,
//         status: props.info.status
//     }
//     emit('handleChangeStatus', data,'')
// }

function handleToActive(): void {
    var data = {
        id: props.info.id,
        title: props.info.title,
        status: props.info.status
    }
    emit('toActive', data,'')
};

function handleToCompleted(): void {
    var data = {
        id: props.info.id,
        title: props.info.title,
        status: props.info.status
    }
    emit('toCompleted', data, '')
};

function handletoHasDueDate(): void {
    var data = {
        id: props.info.id,
        title: props.info.title,
        status: props.info.status
    }
    emit('toHasDueDate', data,'')
};
        
    
</script>

<template>
    
            <!-- Todo Item 1 -->
        <div v-if="props.info.status == 'Completed'">
            <div class="row px-3 align-items-center todo-item rounded">
                <div class="col-auto m-1 p-0">
                    <h2 class="">
                        <i class="far fa-check-square checkbox-check mt-2 text-primary" style="justify-content: right; cursor: pointer;"></i>
                    </h2>
                </div>
                <div class="col px-1 m-1">
                    <input type="text" class="form-control form-control-lg border-0 edit-todo-input bg-transparent rounded px-3" disabled v-bind:value="props.info.title">
                </div>
                <div class="col-auto m-1 p-0 todo-actions">
                    <div class=" todo-action-icons">
                        <div class="" style="margin-right: 10px;" v-on:click="handletoHasDueDate">
                            <i class="fas fa-edit text-primary btn m-0 p-0 todo-action-icons-item"></i>
                        </div>
                        <div class="" v-on:click="handleDelete">
                            <i class="fas fa-trash-alt text-danger btn m-0 p-0 todo-action-icons-item"></i>
                        </div>
                    </div>
                    <div class="row todo-created-info">
                        <div class="col-auto d-flex align-items-center pr-2">
                            <i class="fas fa-info-circle my-2 px-2 text-black-50 btn"></i>
                            <label class="date-label my-2 text-black-50">28th Jun 2020</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>


            <!-- Todo Item 2 -->
        <div v-if="props.info.status == 'Active'">
            <div class="row px-3 align-items-center todo-item rounded">
                <div class="col-auto m-1 p-0">
                    <h2 class="">
                        <i v-on:click="handleToCompleted" class="far fa-square checkbox-check mt-2 text-primary" style="justify-content: right; cursor: pointer;"></i>
                    </h2>
                </div>
                <div class="col px-1 m-1">
                    <input v-bind:value="props.info.title" type="text" class="form-control form-control-lg border-0 edit-todo-input bg-transparent rounded px-3" disabled>
                </div>
                <div class="col-auto m-1 p-0 px-3 time-list">
                    <div class="row">
                        <div class="col-auto d-flex align-items-center rounded bg-white border border-warning">
                            <i class="fas fa-hourglass my-2 px-2 text-warning btn"></i>
                            <h6 class="text my-2 pr-2">28th Jun 2020</h6>
                        </div>
                    </div>
                </div>
                <div class="col-auto m-1 p-0 todo-actions">
                    <div class=" todo-action-icons">
                        <div class="" style="margin-right: 10px;" v-on:click="handletoHasDueDate">
                            <i class="fas fa-edit text-primary btn m-0 p-0 todo-action-icons-item"></i>
                        </div>
                        <div class="" v-on:click="handleDelete">
                            <i class="fas fa-trash-alt text-danger btn m-0 p-0 todo-action-icons-item"></i>
                        </div>
                    </div>
                    <div class="row todo-created-info">
                        <div class="col-auto d-flex align-items-center pr-2">
                            <i class="fas fa-info-circle my-2 px-2 text-black-50 btn"></i>
                            <label class="date-label my-2 text-black-50">28th Jun 2020</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>

            <!-- Todo Item 3 -->
        <div v-if="props.info.status == 'Has-due-date'">
            <div class="row px-3 align-items-center todo-item rounded">
                <div class="col-auto m-1 p-0">
                    <h2 class="">
                        <i v-on:click="handleToActive" class="far fa-square checkbox-check mt-2 text-primary" style="justify-content: right; cursor: pointer;"></i>
                    </h2>
                </div>
                <div class="col px-1 m-1">
                    <input type="text" class="form-control form-control-lg border-0 edit-todo-input bg-transparent rounded px-3" v-model="props.info.title">
                </div>
                <div class="col-auto m-1 p-0 todo-actions">
                    <div class=" todo-action-icons">
                    
                        <div class="">
                            <i v-on:click="handleDelete" class="fas fa-trash-alt text-danger btn m-0 p-0 todo-action-icons-item"></i>
                        </div>
                    </div>
                    <div class="row todo-created-info">
                        <div class="col-auto d-flex align-items-center pr-2">
                            <i class="fa-solid fa-circle-info my-2 px-2 text-black-50 btn"></i>
                            <label class="date-label my-2 text-black-50">28th Jun 2020</label>
                        </div>
                    </div>
                </div>
            </div>
        </div>
</template>

<style scoped>

    .todo-item{
        display: flex;
        align-items: center;
    }

    .todo-actions {
        visibility: hidden !important;
    }
    
    .todo-action-icons{
        display: flex;
        justify-content: right;
        flex-direction: row;
    }

    .todo-action-icons-item{
        font-size: 25px;

    }


    @media (max-width: 739px){
        .time-list{
            display: none;
        }
    }
    .todo-item:hover .todo-actions{
        visibility: visible !important;
    }
    .todo-created-info{
        display: flex;
        justify-content: right;
    }
</style>