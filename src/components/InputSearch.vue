<script>
export default {
    props:{
        modelValue: { type: String, default: "" },
    },
    emits: ["submit", "update:modelValue"],
    methods: {
        updateModelValue(e) {
            this.$emit("update:modelValue", e.target.value);
        },
        submit() {
            this.$emit("submit");
        },
    }, 
};
</script>

<template>

    <form class="d-flex" style="background-color: gray-200">
        <input class="form-control me-2" type="search" placeholder="Nhập tên nhân viên" aria-label="Search" :value="modelValue" 
@input="updateModelValue" @keyup.enter="submit" >
        <button class="btn btn-outline-success" type="button" @click="submit">Search</button>
      </form>
</template>