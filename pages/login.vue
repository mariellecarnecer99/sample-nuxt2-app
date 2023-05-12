<template>
    <v-sheet width="500" class="mx-auto">
        <h1 class="text-center my-5"><v-icon icon="mdi-contacts"></v-icon> Contact Keeper</h1>
        <v-alert v-if="error && error.length" color="red" type="error" class="mb-4">{{ this.error }}</v-alert>
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

            <v-container>
                <v-row justify="center" align="center">
                    <v-col>
                        <v-btn
                            color="primary"
                            class="mt-4"
                            block
                            @click.prevent="onSubmit"
                            type="submit"
                        >
                        Login
                        </v-btn>
                    </v-col>
                </v-row>
            </v-container>
        </v-form>
    </v-sheet>
</template>

<script>
// This will work in both `<script setup>` and `<script>`
definePageMeta({
  layout: "login",
});

export default {
    data() {
        return {
            email: '',
            password: '',
            error: ''
        };
    },
    methods: {
        onSubmit() {
            const router = useRouter();
            const { email, password } = this;

            try {
                this.error = '';

                if(!!email === false || !!password === false) {
                    this.error = 'Please enter the required fields.';
                    return;
                }

                localStorage.setItem('userEmail', email);

                router.push({path: "/"});
            } catch (error) {
                if (error) {
                    this.error = 'Invalid credentials';
                }
            }
        }
    }
}
</script>