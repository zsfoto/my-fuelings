<template>
<f7-page name="about">
    <f7-navbar :title="`${mainTitle}`" back-link="Back"></f7-navbar>
    <f7-block-title><h1>{{ title }}</h1></f7-block-title>
    <f7-block>
        <div v-html="`${body}`"></div>
    </f7-block>
</f7-page>
</template>

<script>
import { ref } from 'vue'

export default {

    setup() {
        const mainTitle = ref('')
        const title = ref('Title')
        const body = ref('<p>Lorem <b>ipsum</b> dolor sit amet, <u>consectetur adipisicing</u> elit.</p> <p>Magni molestiae laudantium dignissimos est nobis delectus nemo ea alias voluptatum architecto, amet similique, saepe iste consectetur in repellat ut minus quibusdam!</p>')

        return {
            mainTitle,
            title,
            body
        }
    }
}
</script>
