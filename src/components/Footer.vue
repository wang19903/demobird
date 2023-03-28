<template>
    <footer>
        <p>&copy;hao 2023 demo</p>
        <a href="mailto:lf21715@yahoo.com.tw">contact me!</a>
    </footer>
</template>

<style lang="scss" scoped>
footer {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;

    a {
        color: #000;
        margin: 16px;

        &:active {
            transform: scale(.95);
        }
    }
}
</style>