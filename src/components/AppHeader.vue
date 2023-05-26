<template>
    <header>
        <div class="container">
            <div class="d-flex justify-content-between">
                <div class="logo">Projects</div>
                <nav>
                    <ul class="list-unstyled m-0 p-0 gap-3 d-flex">
                        <li>
                            <RouterLink :to="{ name: 'home' }" class="nav-link">
                                home
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink :to="{ name: 'projects' }" class="nav-link">
                                projects
                            </RouterLink>
                        </li>
                        <li>
                            <RouterLink :to="{ name: 'about' }" class="nav-link">
                                About
                            </RouterLink>
                        </li>
                    </ul>
                </nav>
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: 'AppHeader'
}
</script>

<style scoped>
header {
    padding: 20px;
    background-color: rgb(119, 241, 170);
}
</style>