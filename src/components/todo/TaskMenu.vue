<template>
    <div>
        <v-menu bottom left>
        <template v-slot:activator="{ on, attrs }">
            <v-btn icon color="primary" v-bind="attrs" v-on="on">
                <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
        </template>

        <v-list>
            <v-list-item v-for="(item, index) in items" 
            :key="index"
            @click="handleClick(index)">
                <v-list-item-icon>
                    <v-icon v-text="item.icon"></v-icon>
                </v-list-item-icon>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
        </v-list>
    </v-menu>
         <dialog-edit 
                v-if="dialogs.edit"
                :task="task"
                @close="(dialogs.edit = false)"
                >
        </dialog-edit>
        <dialog-due-date 
                v-if="dialogs.dueDate"
                :task="task"
                @close="(dialogs.dueDate = false)"
                >
        </dialog-due-date>
        <dialog-delete 
                v-if="dialogs.delete"
                :task="task"
                @close="(dialogs.delete = false)"
                >
        </dialog-delete>
    </div>
   
</template>

<script>
export default {
    props: ['task'],
    data: () => ({
        dialogs: {
                edit: false,
                dueDate: false,
                delete: false,

            },
        items: [
            { 
                title: 'Edit',
                icon: 'mdi-pencil',
                click() {
                    this.dialogs.edit = true
                }
            },
            { 
                title: 'Due date',
                icon: 'mdi-calendar',
                click() {
                    this.dialogs.dueDate = true
                }
             },
            {
                 title: 'Delete',
                 icon: 'mdi-delete',
                 click() {
                   this.dialogs.delete = true
                }
            },
            {
                 title: 'Sort',
                 icon: 'mdi-drag-horizontal-variant',
                 click() {
                    if (!this.$store.state.search) {
                        this.$store.commit('toggleSorting')
                    }
                    else {
                        this.$store.commit('showSnackbar', 'No sorting while searching')
                    }
                  
                }
            },
        ],
    }),
    methods: {
        handleClick(index) {
            this.items[index].click.call(this)
        }
    },
    components: {
        'dialog-edit': require('@/components/todo/Dialogs/DialogEdit.vue').
         default,
        'dialog-due-date': require('@/components/todo/Dialogs/DialogDueDate.vue').
         default,
        'dialog-delete': require('@/components/todo/Dialogs/DialogDelete.vue').
         default,    
    }
}
</script>

<style>

</style>