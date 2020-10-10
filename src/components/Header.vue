<template>
    <div>
        <b-navbar toggleable="lg" type="dark" variant="info">
            <b-navbar-brand href="#">Dashboard</b-navbar-brand>

            <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

            <b-collapse id="nav-collapse" is-nav>
            <b-navbar-nav>
                <b-nav-item href="#">Contacto</b-nav-item>                
            </b-navbar-nav>

            
            </b-collapse>
        </b-navbar>
    </div>
</template>

<script>   

    export default {
        name: 'Header'
    }
</script>

<style scoped>

</style>