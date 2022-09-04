<script lang="ts">
import { defineComponent, PropType } from "vue";
import TodoListSectionComp from "./TodoListSectionComp.vue";
export default defineComponent({
    name: "ListInfoComp",
    components: {
        TodoListSectionComp
    },
    props: {
        listInfo: {
            type: Array as any,
            default: ''
        }
    },
    data() {
        return{
            filterSelect: '',
            selected: ''
        }
    },
    methods: {
        deleteInfo(data: any) {
            this.$emit("deleteInfoEvent", data);
            console.log(this.listInfo)
        },
        toActive(data: any) {
            this.$emit("toActiveEvent", data);
        },
        toCompleted(data: any) {
            this.$emit("toCompletedEvent", data);
        },
        toHasDueDate(data: any) {
            this.$emit("toHasDueDateEvent", data);
        },
        toFilterEvent(data: any) {
            console.log(data.filterSelect, "123");
        },
    },
    computed: {
        filterInfo() {
            const oppsitethat = this;
            if (oppsitethat.filterSelect == "All" || oppsitethat.filterSelect == "") {
                return (this.listInfo)
            }
            else {
                return (
                    this.listInfo.filter(function (item: any) {
                        return item.status == oppsitethat.filterSelect
                    })
                );
            }
        }
    }
})
</script>

<template>
    <div class="row m-1 p-3 px-5 justify-content-end">
        <div class="col-auto d-flex align-items-center">
            <label class="text-secondary my-2 pr-2 view-opt-label">Filter</label>
            <select class="select-css custom-select custom-select-sm btn my-2" v-model="filterSelect">
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
                    v-on:toFilterEvent="toFilterEvent"></TodoListSectionComp>
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