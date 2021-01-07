<template>
    <form @submit.prevent="sendFile" enctype="multipart/form-data">
        <div class="field">
            <div class="file is-boxed is-primary">
                <label class="file-label">
                    <input
                        type="file"
                        ref="file"
                        @change="selectFile"
                        class="file-input"
                        />
                    <span class="file-cta">
                        <span class="file-icon">
                            <i class="fas fa-upload"></i>
                        </span>
                        <span class="file-label">
                            Choose a file...
                        </span>
                    </span>
                    <span v-if="form.file" class="file-name">{{form.file.name}}</span>
                </label>
            </div>
        </div>
        <div class="field">
            <input v-model="form.test">
        </div>
        <div class="field">
            <input v-model="form.testTwo">
        </div>
        <div class="field">
            <button class="button is-info">Send</button>
        </div>
    </form>
</template>

<script>
    import axios from "axios"
    export default {
        name: "SimpleUpload",
        data(){
            return {
                form: {
                    file: "",
                    test: "",
                    testTwo: ""
                }
            }
        },
        methods: {
            selectFile(){
                this.form.file = this.$refs.file.files[0]
            },
            async sendFile(){
                const formData = new FormData();
                formData.append("file", this.form.file)
                formData.append("test", this.form.test)
                formData.append("testTwo", this.form.testTwo)
                try{
                    console.log(formData)
                    await axios.post("/upload", formData)
                } catch(err){
                    console.log(err)
                }
            }
        }
    }
</script>