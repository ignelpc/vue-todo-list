<template>
<div class="form-group mb-3">
    <label :for="name">{{label}}</label>
    <input :type="type" class="form-control" :name="name" :id="name" :placeholder="placeholder" :v-model="model" :value="value">
</div>
</template>

<script>
export default {
    name: 'Input',
    props: {
        type: String,
        name: String,
        model: String,
        placeholder: String,
        label: String,
        value: String
    },
    data() {
        return {

        }
    }
}
</script>
