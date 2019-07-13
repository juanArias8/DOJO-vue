<template>
    <div id="translateIn">
        <p>Translation</p>
        <form v-on:submit="formSubmit">
            <input type="text" v-model="text" placeholder="escriba la palabra">
            <select v-model="language">
                <option disabled value="">Idioma a traducir</option>
                <option value="en">Inglés</option>
                <option value="fr">Frances</option>
                <option value="it">Italiano</option>
            </select>
            <input type="submit" value="Traducir">
        </form>

        <p>Traducción...</p>
        <p>{{translatedText}}</p>
    </div>
</template>

<script>
    export default {
        name: "Translate",
        data() {
            return {
                text: '',
                language: 'en',
                translatedText: ''
            }
        },
        methods: {
            formSubmit(e) {
                this.$http.get(`https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20190622T213455Z.f67e95598c7aee64.c0c49d0594aa527178d83c8e3c1a81ed05709a56&lang=${this.language}&text=${this.text}`)
                    .then((response) => {
                        this.translatedText = response.body.text[0];
                    });
                e.preventDefault();
            },
        }
    }
</script>

<style scoped>

</style>
