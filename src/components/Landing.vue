<script>

</script>

<template>
    <section class="landing-section">
        <div class="overlay">
            <div class="page-content">
                <div class="page-tittle">
                    <div>
                        <img src="../assets/vue.svg" alt="Vue svg">
                        <h1>Vue</h1>
                    </div>
                    <h1>Restaurant</h1>
                </div>
                <div class="authors">
                    <a href="https://github.com/PabloGoProg" target="_blank">
                        <img src="../assets/github.svg" alt="Github svg">
                        Pablo Gonzalez
                    </a>
                    <a href="https://github.com/Jimmygm16" target="_blank">
                        <img src="../assets/github.svg" alt="Github svg">
                        Jimmy Alexander Giraldo
                    </a>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
    .landing-section {
        background: url(../assets/background.jpg);
        background-size: cover;
        background-position: center;
        height: 100vh;

        .overlay {
            background-color: rgba(0, 0, 0, 0.4);
            height: 100vh;

            .page-content {
                display: flex;
                justify-content: center;
                flex-direction: column;
                height: 100vh;

                .page-tittle {
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    height: 100%;
                    font-size: 4rem;
                    font-family: 'Roboto', sans-serif;
                    gap: 1rem;

                    div {
                        display: flex;
                        align-items: center;
                        justify-content: center;

                        h1 {
                            color:#41B883;
                        }
                    }

                    img {
                        width: 10rem;
                        height: 10rem;
                    }

                    h1 {
                        color: white;
                        margin-top: 0.5rem;
                    }
                }

                .authors {
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    gap: 1rem;
                    position: relative;
                    bottom: 19rem;
                    font-family: 'Roboto', sans-serif;
                    color: white;
                    text-align: center;
                    font-size: 1.2rem;

                    a {
                        color: #41B883;
                        text-decoration: none;
                        text-align: center;
                        background-color: white;
                        padding: 0.2rem 0.4rem;
                        border-radius: 6px;
                        transition: ease-in-out 0.3s;
                    }

                    img {
                        width: 1.2rem;
                        height: 1.2rem;
                    }

                    a:hover {
                        background-color: #41B883;
                        color: white;
                    }
                }
            }
        }
    }
</style>
import { h } from 'vue';
