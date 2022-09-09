<script setup lang="ts">
import { computed , reactive,PropType} from "vue";
import { Info } from "../interfaces/interfaces";
import TodoListSectionComp from "./TodoListSectionComp.vue";

const props = defineProps<{
    listInfo: Info[]
}>(
    
)


const emit = defineEmits<{
    (e: "statusChange",data: Info ,status: string): void
    (e: "deleteInfo",data: Info): void
}>()
    
const dataReturn = reactive({
    filterSelect: '',
    selected: ''
});


function deleteInfo(data: Info) {
    emit("deleteInfo",data);
};

function toActive(data: Info, status: string) {
    emit("statusChange", data, "Active");
};

function toCompleted(data: Info, status: string) {
    emit("statusChange", data, "Completed");
};

function toHasDueDate(data: Info, status: string) {
    emit("statusChange", data, "Has-due-date");
};

//computed callback
function filterInfo1() {
    const sizeFilter = dataReturn;
    if (sizeFilter.filterSelect == "All" || sizeFilter.filterSelect == "") {
        return (props.listInfo)
    }
    else {
        return (
            props.listInfo.filter(function (item: Info) {
                return item.status == sizeFilter.filterSelect
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