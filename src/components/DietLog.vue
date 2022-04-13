<template>
    <md-table-row>
  
    <md-table-cell>{{log.date}}</md-table-cell>
    <md-table-cell>{{log.time}}</md-table-cell>
    <md-table-cell>{{log.category}}</md-table-cell>
    <md-table-cell>{{log.name}}</md-table-cell>
    <md-table-cell>{{log.weight}}</md-table-cell>
    <md-table-cell>{{log.calories}}</md-table-cell>

    </md-table-row>

</template>
<script>

export default({
    props: ['log']

})
</script>
