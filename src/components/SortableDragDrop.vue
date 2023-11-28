<template>
    <main class="main-card">
        <div class="container-fluid mt-5">
            <div class="text-center text-light h1">Sortable drag drop</div>
            <div class="row">
                <div class="col form-inline">
                    <b-form-input id="input-2" v-model="newTask" required placeholder="Enter Task"
                        @keyup.enter="add"></b-form-input>
                    <b-button @click="add" variant="primary" class="ml-3">Add</b-button>
                </div>
            </div>
            <div class="row mt-5">
                <div class="col-3">
                    <Card :cardHeading="'BACK LOG'" :cardColor="'alert-warning'">
                        <draggable class="list-group sortable-drag-column" :list="arrBackLog" group="tasks"
                            @end="handleDragEnd">
                            <List v-for="element in arrBackLog" :key="element.name" :name="element.name" />
                        </draggable>
                    </Card>
                </div>
                <div class="col-3">
                    <Card :cardHeading="'IN PROGRESS'" :cardColor="'alert-success'">
                        <draggable class="list-group sortable-drag-column" :list="arrInProgress" group="tasks"
                            @end="handleDragEnd">
                            <List v-for="element in arrInProgress" :key="element.name" :name="element.name" />
                        </draggable>

                    </Card>
                </div>
                <div class="col-3">
                    <Card :cardHeading="'TESTING'" :cardColor="'alert-danger'">
                        <draggable class="list-group sortable-drag-column" :list="arrTested" group="tasks"
                            @end="handleDragEnd">
                            <List v-for="element in arrTested" :key="element.name" :name="element.name" />
                        </draggable>
                    </Card>
                </div>
                <div class="col-3">
                    <Card :cardHeading="'DONE'" :cardColor="'alert-primary'">
                        <draggable class="list-group sortable-drag-column" :list="arrDone" group="tasks"
                            @end="handleDragEnd">
                            <List v-for="element in arrDone" :key="element.name" :name="element.name" />
                        </draggable>
                    </Card>
                </div>
            </div>
        </div>
    </main>
</template>
<script>

import Card from "./Card.vue";
import List from "./List.vue";
import draggable from "vuedraggable";
export default {
    name: "sortable-drag-drop",
    components: {
        Card,
        draggable,
        List

    },
    data() {
        return {
            newTask: "",
            arrBackLog: [],
            arrInProgress: [],
            arrTested: [],
            arrDone: []
        };
    },
    created() {
        this.loadTaskOrders();
    },
    methods: {
        add() {

            if (this.newTask) {
                this.arrBackLog.push({ name: this.newTask });
                this.newTask = "";
                this.saveTaskOrders();
            }
        },
        saveTaskOrders() {

            localStorage.setItem("taskOrders", JSON.stringify({
                arrBackLog: this.arrBackLog,
                arrInProgress: this.arrInProgress,
                arrTested: this.arrTested,
                arrDone: this.arrDone
            }));


        },
        loadTaskOrders() {
            const savedOrders = localStorage.getItem("taskOrders");
            if (savedOrders) {
                const parsedOrders = JSON.parse(savedOrders);
                this.arrBackLog = parsedOrders.arrBackLog || [];
                this.arrInProgress = parsedOrders.arrInProgress || [];
                this.arrTested = parsedOrders.arrTested || [];
                this.arrDone = parsedOrders.arrDone || [];
            }
        },
        handleDragEnd() {
            this.saveTaskOrders();
        }
    }
};
</script>
