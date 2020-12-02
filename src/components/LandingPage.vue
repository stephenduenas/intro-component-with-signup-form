<template>
    <main class="main-section container">
        <div class="main">
            <h1 class="main__title">Learn to code by watching others</h1>
            <p class="main__description">See how experienced developers solve problems in real-time. Watching scripted tutorials is great, 
            but understanding how developers think is invaluable.</p>
        </div>
        <div class="signup-section">
            <div class="signup__notification">
                <p class="signup__notification--text">
                    <b>Try it free 7 days</b>  then $20/mo. thereafter
                </p>
            </div>
            <SignUpForm></SignUpForm>
        </div>
    </main>
</template>

<script>
import SignUpForm from './SignUpForm'

export default {
    components: {
        SignUpForm,
    }
}
</script>