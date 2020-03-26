<template>
    <div>
        <v-card
            class="pa-3"
            :class="{'done' : list.status === 'done'}"
            v-for="(list, index) in todoList"
            :key="index"
        >
            <p>{{ list.memo }}</p>
            <p>{{ list.status }}</p>
            <v-btn 
                v-if="list.status === 'created'"
                @canplaythrough="$emit('statusControl', index, 'done')"
                fab flat small color="green"
            >완료</v-btn>
            <v-btn 
                v-else
                @click="$emit('statusControl', index, 'created')"
                fab 
            >부활</v-btn>
            <v-btn 
                @click="$emit('listDelete', index)"
                fab
            >제거</v-btn>
            <v-btn
                @click="listEdit()"
                v-if="list.status === 'created'"
                fab flat small color="yellow"
            >수정</v-btn>
        </v-card>
    </div>
</template>

<script>
import { eventBus } from '../main'
export default{
    props: ['todoList'],
    methods: {
        listEdit(memo, index) {
            eventBus.listEdit(memo, index)
        }
    }
}
</script>

<style scoped>
.done{ background-color: rgba(0, 0, 0, .1); }
.done p{
    text-decoration: line-through;
    color:rgba(0, 0, 0, .5);
}
</style>