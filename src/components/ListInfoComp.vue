<script setup lang="ts">
import { computed , reactive} from "vue";
import TodoListSectionComp from "./TodoListSectionComp.vue";
import { Info } from '../interfaces/interfaces';
import { defineProps, defineEmits } from "vue";

name: "ListInfoComp";

const props = defineProps({
    listInfo: {
        type: Object,
        default: () => []
    }
})

const emit = defineEmits(['deleteInfoEvent','toActiveEvent','toCompletedEvent','toHasDueDateEvent' ])
    

        const dataReturn = reactive({
            filterSelect: '',
            selected: ''
        });


        function deleteInfo(data: Info) {
            emit("deleteInfoEvent", data);
        };

        function toActive(data: Info) {
            emit("toActiveEvent", data);
        };

        function toCompleted(data: Info) {
            emit("toCompletedEvent", data);
        };

        function toHasDueDate(data: Info) {
            emit("toHasDueDateEvent", data);
        };

        //computed callback
        function filterInfo1() {
            const oppsitethat = dataReturn;
            if (oppsitethat.filterSelect == "All" || oppsitethat.filterSelect == "") {
                return (props.listInfo)
            }
            else {
                return (
                    props.listInfo.filter(function (item: Info) {
                        return item.status == oppsitethat.filterSelect
                    })
                );
            }
        }

        const filterInfo = computed(() => filterInfo1())

       
</script>

<template>
    <div class="row m-1 p-3 px-5 justify-content-end">
        <div class="col-auto d-flex align-items-center">
            <label class="text-secondary my-2 pr-2 view-opt-label">Filter</label>
            <select class="select-css custom-select custom-select-sm btn my-2" v-model="dataReturn.filterSelect">
                <option value="" selected>All</option>
                <option value="Completed">Completed</option>
                <option value="Active">Active</option>
                <option value="Has-due-date">Has due date</option>
            </select>
        </div>
        <div class="col-auto d-flex align-items-center px-1 pr-3">
            <label class="text-secondary my-2 pr-2 view-opt-label">Sort</label>
            <select class="select-css custom-select custom-select-sm btn my-2">
                <option value="added-date-asc" selected>Added date</option>
                <option value="due-date-desc">Due date</option>
            </select>
            <i class="fas fa-sort-amount-down-alt text-info " style="margin-left: 10px; font-size: 20px"></i>
        </div>
    </div>
    <div class="row mx-1 px-5 pb-3 w-80">
        <div class="col mx-auto">
    <TodoListSectionComp v-for="info in filterInfo" :key="info.id" :info="info" @deleteInfo="deleteInfo"
                    @toActive="toActive" @toCompleted="toCompleted" @toHasDueDate="toHasDueDate"
                    ></TodoListSectionComp>
        </div>
    </div>
</template>
    
<style scoped>
    .select-css{
        border: solid 1px #ccc;
        margin-left: 3px;
    }
    
    
    .select-css option:hover{
        background-color: gray;
    }
</style>