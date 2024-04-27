<template>
    <div>
        <h3>Permissions</h3>
        <hello-world
                endpoint="/permissions"
                :columns="['name','action']"
                :form-fields="{
                name: ''
            }"
        >
            <!-- your form input fields in this slot-->
            <template v-slot:input-fields="{formdata}">
                <b-form-group id="input-group-2" label="Your Name:" label-for="input-2">
                    <b-form-input
                            id="input-2"
                            v-model="formdata.name"
                            required
                            placeholder="Enter name"
                    ></b-form-input>
                </b-form-group>
            </template>
        </hello-world>

    </div>
</template>

<script>
import HelloWorld from './HelloWorld.vue';

    export default {
        components: {HelloWorld},
    };
</script>