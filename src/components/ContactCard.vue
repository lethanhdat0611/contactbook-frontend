<script>
export default{
    props:{
        contact: { type: Object, required: true },
    } , 
};
</script>
<template>
    <div>
        <div class="p-1">
            <strong>Tên:</strong>
            {{ contact.name }}
        </div>
        <div class="p-1">
            <strong>E-mail:</strong>
            {{ contact.email }}
        </div>
        <div class="p-1">
            <strong>Gender:</strong>
            {{ contact.gender }}
        </div>
        <div class="p-1">
            <strong>Ngày sinh:</strong>
            {{ contact.birthday }}
        </div>
        <div class="p-1">
            <strong>Công việc:</strong>
            {{ contact.work }}
        </div>
        <div class="p-1">
            <strong>Địa chỉ:</strong> 
            {{ contact.address }}
        </div>
        <div class="p-1">
            <strong>Điện thoại:</strong> 
            {{ contact.phone }}
        </div>
    </div>
</template>