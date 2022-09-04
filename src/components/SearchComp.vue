<script lang="ts">
import { defineComponent, ref, PropType } from 'vue';

export default defineComponent({
    name: "SearchComp",
    props: {
        textInputInfo: {
            type: Object,
            default: () => []
        },
        listInfo: {
            type: Array as any,
            default: () => []
        }
    },
    setup() {
        
    },
    methods: {
        handleAdd(e: object): void{
            var data = {
                text: this.textInputInfo,
            }
            this.$emit('addInfo', data);
            this.textInputInfo.value = "";
        }
    }
    
});

</script>

<template>
<form action="">
    <div class="row m-1 p-3">
        <div class="row bg-white rounded shadow-sm p-2 add-todo-wrapper align-items-center justify-content-center">
            <div class="col">
                <input type="text" class="form-control form-control-lg border-0 add-todo-input bg-transparent rounded" placeholder="Add new..." v-model="textInputInfo.value" />
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