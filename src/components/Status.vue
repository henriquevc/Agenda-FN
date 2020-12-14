<template>
    <div class="row">
        <div class="col-8 ">
            <div class="text-h4">Status</div>
        </div>
        <div class="col-4">{{status}}</div>
    </div>
</template>
<script>
export default {
    props: {
        status: {
            type: String
        }
    }
}
</script>
