<template>
    <div class="row">
        <div class="col-md-6 col-md-offset-3">
            <div class="panel panel-default">
                <div class="panel-body">
                    <div class="form-group">
                        <input
                                v-model="email"
                                class="form-control"
                                type="email"
                                placeholder="Email:">
                    </div>
                    <div class="form-group">
                        <input
                                v-model="password"
                                class="form-control"
                                type="password"
                                placeholder="Password:">
                    </div>

                    <button @click="login" class="btn btn-success pull-right">Login</button>
                </div>
            </div>
        </div>

    </div>
</template>
<style>

</style>
<script>
    export default {
        data () {
            return {
                email: '',
                password: ''
            }
        },
        methods: {
            login () {
                var data = {
                    client_id: 2,
                    client_secret: 'IdZF0R4t1E5h9nPUrylDARjChrO9uc3lmN9XfRNW',
                    grant_type: 'password',
                    username: this.email,
                    password: this.password
                }

                this.$http.post("http://localhost:8000/oauth/token", data)
                        .then(response => {
                            //console.log(response)
                            this.$auth.setToken(response.body.access_token, response.body.expires_in + Date.now())
                        })
            }
        }
    }
</script>