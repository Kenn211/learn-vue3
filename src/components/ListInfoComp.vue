<script lang="ts">
import { defineComponent, PropType,ref, computed , reactive} from "vue";
import TodoListSectionComp from "./TodoListSectionComp.vue";
import { Info } from '../interfaces/interfaces';
export default defineComponent({
    name: "ListInfoComp",
    components: {
        TodoListSectionComp
    },
    props: {
        listInfo: {
            type: Object,
            default: () => []
        }
    },
    
    // data() {
    //     return{
    //         filterSelect: '',
    //         selected: ''
    //     }
    // },

    
    setup(props,context){
        const dataReturn = reactive({
            filterSelect: '',
            selected: ''
        });

        const filterInfo = computed(() => filterInfo1())

        function deleteInfo(data: Info) {
            context.emit("deleteInfoEvent", data);
        };

        function toActive(data: Info) {
            context.emit("toActiveEvent", data);
        };

        function toCompleted(data: Info) {
            context.emit("toCompletedEvent", data);
        };

        function toHasDueDate(data: Info) {
            context.emit("toHasDueDateEvent", data);
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

        return {
            deleteInfo,toActive,toCompleted,toHasDueDate,filterInfo,dataReturn,props,context
        }
    },
    
})
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