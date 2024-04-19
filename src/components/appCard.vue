<template>
    <li class="card">
        <div class="card-body">
            <p>{{ item.title }}</p>
            <p>{{ item.original_title }}</p>
            <img :src="item.flag">
            <p>{{ item.rating }}</p>


            <font-awesome-icon v-for="n in 5" :icon="[n <= item.rating ? 'fas' : 'far', 'star']" />

            <!-- <font-awesome-icon :icon="['far', 'star']" /> -->

            <div>
                <img :src="item.poster" alt="" />
            </div>
        </div>


    </li>

</template>

<script>
export default {
    props: {
        item: {
            type: Object,
            required: true
        },
    },
}
</script>

<style lang="scss" scoped></style>