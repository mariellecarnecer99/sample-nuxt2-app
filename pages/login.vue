<template>
    <v-row style="justify-content: center">
        <v-col cols="5">
            <h1 style="text-align: center; margin: 10px 0"><v-icon large>mdi-contacts</v-icon> Contact Keeper</h1>
            <v-alert v-if="error && error.length" color="red lighten-2" type="error" class="mb-4" style="background-color: red">{{ this.error }}</v-alert>
            <v-form @submit.prevent="onSubmit" @keydown.enter="onSubmit">
                <v-text-field
                    v-model="email"
                    type="text"
                    label="E-mail"
                    placeholder="name@mail.com"
                    outlined
                    required
                ></v-text-field>

                <v-text-field
                    v-model="password"
                    outlined
                    placeholder="**********"
                    type="password"
                    label="Password"
                    required
                ></v-text-field>

                <v-btn
                    color="primary"
                    class="mt-4"
                    block
                    @click.prevent="onSubmit"
                    type="submit"
                    style="background-color: blue"
                >
                    Login
                </v-btn>
            </v-form>
        </v-col>
    </v-row>
</template>

<script>
export default {
    layout: 'login',
    data() {
        return {
            email: '',
            password: '',
            error: ''
        };
    },
    methods: {
        onSubmit() {
            const { email, password } = this;

            try {
                this.error = '';

                if(!!email === false || !!password === false) {
                    this.error = 'Please enter the required fields.';
                    return;
                }

                localStorage.setItem('userEmail', email);

                this.$router.push({path: "/"});
            } catch (error) {
                if (error) {
                    this.error = 'Invalid credentials';
                }
            }
        }
    }
}
</script>