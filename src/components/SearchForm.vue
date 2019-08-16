<template>
    <div>
        <div class="row top-space">
            <div class="col">
                <h5>Поиск</h5>
            </div>
        </div>
        <div class="row">
            <div class="col-6 col-md-4 col-lg-3">
                <label><input type="text" placeholder="По имени или телефону" tabindex="5"></label>
            </div>
            <div class="col-3 col-md-2">
                <button tabindex="6">Найти</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "SearchForm"
    }
</script>

<style scoped>

</style>