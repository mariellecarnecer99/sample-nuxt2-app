<template>
    <v-row justify="center">
        <v-col cols="4">
            <h1 class="text-center my-5">Add Contact</h1>
                <v-form ref="contactForm" @submit.prevent="onSubmit()">
                    <v-text-field
                        v-model="form.name"
                        label="Name"
                        required
                        :rules="nameRules"
                    ></v-text-field>

                    <v-text-field
                        v-model="form.email"
                        label="E-mail"
                        required
                        :rules="emailRules"
                    ></v-text-field>

                    <v-text-field
                        v-model="form.phone"
                        label="Phone"
                        required
                        :rules="phoneRules"
                    ></v-text-field>

                    <v-radio-group
                        label="Contact Type"
                        v-model="form.inline"
                        :rules="checkboxRules"
                    >
                        <v-radio
                            label="Personal"
                            value="Personal"
                        ></v-radio>
                        <v-radio
                            label="Professional"
                            value="Professional"
                        ></v-radio>
                    </v-radio-group>
                    <v-btn
                        color="success"
                        class="mt-4"
                        block
                        type="submit"
                    >
                    {{btnText == false ? 'Add' : 'Update'}}
                    </v-btn>
                    <v-btn
                        color="surface-variant"
                        class="mt-4"
                        block
                        @click="clearForm()"
                    >
                    Clear
                    </v-btn>
                </v-form>
        </v-col>
        <v-col cols="4">
            <v-text-field
                v-if="contactInfo.length"
                label="Filter Contacts"
                density="compact"
                single-line
                hide-details
                variant="solo"
                append-inner-icon="mdi-magnify"
                style="margin: 30px 0"
            ></v-text-field>
            <v-card
                class="mx-auto my-5"
                v-for="(item, i) in contactInfo"
                :key="i"
                :value="item"
            >
                    <v-row justify="space-between">
                        <v-col style="margin: auto 0">
                            <v-icon class="mx-3" color="surface-variant" medium>mdi-account-box</v-icon> {{item?.name}}
                        </v-col>
                        <v-col >
                            <v-chip
                                v-if="item?.inline === 'Personal'"
                                class="ma-2"
                                color="primary"
                                label
                            >
                            {{item?.inline}}
                            </v-chip>
                            <v-chip
                                v-if="item?.inline === 'Professional'"
                                class="ma-2"
                                color="success"
                                label
                            >
                            {{item?.inline}}
                            </v-chip>
                            <span>
                                <v-icon class="mx-2" color="surface-variant" small>mdi-share-variant</v-icon>
                                <v-icon color="surface-variant" small>mdi-star</v-icon>
                            </span>
                        </v-col>
                    </v-row>
                
                <v-card-text>
                    <p><span><v-icon small>mdi-email-open</v-icon></span> {{item?.email}}</p>
                    <p><span><v-icon small>mdi-phone</v-icon></span> {{item?.phone}}</p>
                </v-card-text>

                <v-card-actions>
                    <v-row justify="center" align="center">
                            <v-col>
                                <v-btn
                                  outlined
                                  color="warning"
                                  class="mt-4"
                                  block
                                  @click="updateContact(i)"
                                >
                                Update
                                </v-btn>
                            </v-col>

                            <v-col>
                                <v-btn
                                  outlined
                                  color="error"
                                  class="mt-4"
                                  block
                                  @click="deleteContact(i)"
                                >
                                Delete
                                </v-btn>
                            </v-col>
                        </v-row>
                </v-card-actions>
            </v-card>
        </v-col>
    </v-row>
</template>

<script>
  export default {
    data () {
      return {
        btnText: false,
        contactInfo: [],
        form: {
            inline: null,
            name: null,
            email: null,
            phone: null
        },
        nameRules: [
            value => {
                if (value) return true

                return 'You must enter a name.'
            },
        ],
        emailRules: [
            value => {
                if (value) return true

                return 'E-mail is required.'
            },
            value => {
                if (/.+@.+\..+/.test(value)) return true

                return 'E-mail must be valid.'
            },
        ],
        phoneRules: [
            value => {
                if (value?.length > 9 && /[0-9-]+/.test(value)) return true

                return 'Phone number needs to be at least 9 digits.'
            }
        ],
        checkboxRules: [
            value => {
                if (value) return true

                return 'At least one must be checked.'
            }
        ]
      }
    },
    watch: {
        contactInfo: {
            handler() {
                localStorage.setItem('contactInfo',JSON.stringify(this.contactInfo))
            },
            deep: true
        }
    },
    mounted() {
        if (localStorage.getItem("contactInfo")){
            this.contactInfo = JSON.parse(localStorage.getItem("contactInfo"))
        }
    },
    methods: {
        onSubmit() {
            if(this.btnText !== true) {
                this.contactInfo.push(this.form);
            } else {
                
            }
            
            // this.clearForm();
        },

        updateContact(id) {
            this.btnText = true;
            const filteredInfo = this.contactInfo.filter(function(value, index, arr){
                return index === id;
            });

            filteredInfo.map(x => {
                this.form = x
            })
        },

        deleteContact(id) {
            this.contactInfo = this.contactInfo.filter(function(value, index, arr){ 
                return index !== id;
            });
        },

        clearForm() {
            this.form = {}
            this.btnText = false;
        }
    }
  }
</script>