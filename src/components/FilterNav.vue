<template>
    <div>
        <nav class="filter-nav">
            <button 
                @click="updateFilter('all')" 
                :class="{ active : current === 'all' }" 
            >View All</button>

            <button 
                @click="updateFilter('completed')" 
                :class="{ active : current === 'completed' }" 
            >Completed</button>

            <button 
                @click="updateFilter('ongoing')" 
                :class="{ active : current === 'ongoing' }" 
            >Ongoing</button>
        </nav>
    </div>
</template>

<script>
export default {
    props : ['current'],
    methods : {
        updateFilter(filterBy){
            this.$emit('filterChanged', filterBy)
        }
    }
}
</script>

<style scoped>
    button{
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
        text-transform: uppercase;
        font-size: 12px;
    }
    button.active{
        color: black;
        padding-bottom: 3px;
        border-bottom: 3px solid #00ec89;
        font-size: 14px;
    }
</style>