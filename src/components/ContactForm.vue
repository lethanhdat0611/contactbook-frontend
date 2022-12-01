<template>
    <Form
        @submit="submitContact"
        :validation-schema="contactFormSchema"
    >
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Tên</span>
            <Field name="name" type="text" class="form-control" placeholder="Nhập tên nhân viên"  aria-describedby="basic-addon1" v-model="contactLocal.name"/>
            
        </div>
   
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Ngày sinh</span>
            <Field name="birthday" type="date" class="form-control" placeholder="Nhập ngày sinh" aria-label="Userbirthday" aria-describedby="basic-addon1" v-model="contactLocal.birthday"/>
            
        </div>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Công việc</span>
            <Field name="work" type="text" class="form-control" placeholder="Nhập tên công việc" aria-label="Userwork" aria-describedby="basic-addon1" v-model="contactLocal.work"/>  
        </div>
        <div class="form-check">
            <Field v-model="contactLocal.gender" class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault1" value="Nam"/>
            <label class="form-check-label" for="flexRadioDefault1">
                Nam
            </label>
          </div>
          <div class="form-check">
            <Field v-model="contactLocal.gender"  class="form-check-input" type="radio" name="flexRadioDefault" id="flexRadioDefault2" value="Nữ" checked/>
            <label class="form-check-label" for="flexRadioDefault2">
                Nữ
            </label>
          </div>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Email</span>
            <Field name="email" type="email" class="form-control" placeholder="Nhập Email" aria-label="Useremail" aria-describedby="basic-addon1" v-model="contactLocal.email" />
        </div>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Địa chỉ</span>
            <Field name="address" type="text" class="form-control" placeholder="Nhập Địa chỉ" aria-label="Useraddress" aria-describedby="basic-addon1" v-model="contactLocal.address"/>
        </div>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Điện thoại</span>
            <Field name="phone" type="tel" class="form-control" placeholder="Nhập Điện thoại" aria-label="Userphone" aria-describedby="basic-addon1" v-model="contactLocal.phone"/>
        </div>

        <div class="form-group">
            <button class="btn btn-primary">Lưu</button>
            <button
                v-if="contactLocal._id"
                type="button"
                class="ml-2 btn btn-danger"
                @click="deleteContact"
            >
                Xóa
            </button>
        </div>
    </Form>
</template>

<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";

export default {
    components: {
        Form,
        Field,
        ErrorMessage,
    },
    emits: ["submit:contact", "delete:contact"],
    props: {
        contact: { type: Object, required: true }
    },
    data() {
        const contactFormSchema = yup.object().shape({
            name: yup
                .string()
                .required("Tên phải có giá trị.")
                .min(2, "Tên phải ít nhất 2 ký tự.")
                .max(50, "Tên có nhiều nhất 50 ký tự."),
            email: yup
                .string()
                .email("E-mail không đúng.")
                .max(50, "E-mail tối đa 50 ký tự."),
            address: yup.string().max(100, "Địa chỉ tối đa 100 ký tự."),
            phone: yup
                .string()
                .matches(
                    /((09|03|07|08|05)+([0-9]{8})\b)/g,
                    "Số điện thoại không hợp lệ."
                ),
        });
        return {
            // Chúng ta sẽ không muốn hiệu chỉnh props, nên tạo biến cục bộ
            // contactLocal để liên kết với các input trên form
            contactLocal: this.contact,
            contactFormSchema,
        };
    },
    methods: {
        submitContact() {
            this.$emit("submit:contact", this.contactLocal);
        },
        deleteContact() {
            this.$emit("delete:contact", this.contactLocal.id);
        },
    },
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>    