<template>
    <div>
        ...
    </div>
</template>

<script>
    export default {
        mounted() {
            this.refresh();
        },

        methods: {
            async refresh() {
                try {
                    await axios.post('/api/login', {
                            username: 'alice@example.com',
                            password: 'secret',
                        })
                        .then(response => {
                            console.log('login');
                            console.log(response.status, response.statusText);
                        });

                    await axios.get('/api/user')
                        .then(response => {
                            console.log('user');
                            console.log(response.status, response.statusText);
                            console.log(response.data);
                        })

                    await axios.post('/api/logout')
                        .then(response => {
                            console.log('logout');
                            console.log(response.status, response.statusText);
                        });
                } catch (error) {
                    console.log(error);
                }
            },
        },
    }
</script>
