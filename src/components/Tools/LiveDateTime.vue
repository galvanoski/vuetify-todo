<template>
   <div class="subtitle-1 ml-4">
          {{ date }}
    </div>
</template>

<script>
import { format, compareAsc } from 'date-fns'

export default {
    data() {
        return {
            date: ''
        }
    },
    methods: {
        getDate() {
           this.date = format(new Date(), 'MMMM d, H:mm:ss')
           setTimeout(this.getDate, 1000)
        }
    },
    mounted() {
        this.getDate()
    }
}
</script>

<style>

</style>