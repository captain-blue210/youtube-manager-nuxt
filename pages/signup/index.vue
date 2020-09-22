<template>
    <div class="section">
        <div class="columns">
            <div class="columns is-6">
                <div class="box">
                    <div class="field">
                        <label for="" class="label">Email</label>
                        <div class="control"
                            ><input
                                v-model="email"
                                class="input is-info"
                                type="email"
                                placeholder="Email"
                            >
                        </div>
                    </div>
                    <div class="field">
                        <label for="" class="label">
                            Password
                            <div class="control">
                                <input
                                    v-model="password"
                                    class="input is-info"
                                    type="password"
                                    placeholder="Password"
                                >
                            </div>
                        </label>
                    </div>
                    <div class="field is-grouped">
                        <div class="control">
                            <button
                                class="button is-link"
                                @click="signUp"
                            >Sign up</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            email: "",
            password: ""
        }
    },
    methods: {
        signUp() {
            let user = {
                email: this.email,
                password: this.password
            }
            this.$store.dispatch('signUp', user)
        }
    }
}
</script>
