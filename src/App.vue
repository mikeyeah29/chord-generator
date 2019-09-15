<template>
    <div id="app">
        <header class="py-3">
            <div class="container">
                <h1 class="text-center display-3 mb-0">Chord Generator</h1>
            </div>    
        </header>

        <div class="main_section">
            <div class="container">
                <div class="row d-flex justify-content-center">
                    <div class="col-sm-6 d-flex justify-content-center">
                        <chord-form @chordsGenerated="onChordsGenerated"></chord-form>
                    </div>
                </div>
            </div>
        </div>

        <div class="container">
            <div class="row d-flex justify-content-center">
                <div class="col-sm-8">
                     <chord-chart :chords="chords" :cgkey="cgkey"></chord-chart>
                </div>
            </div>
        </div>

    </div>
</template>

<script>

    import ChordForm from './components/ChordForm.vue';
    import ChordChart from './components/ChordChart.vue';

    export default {
        name: 'app',
        components: {
            ChordForm, ChordChart
        },
        mounted() {
            axios.get('http://chordgenapi.rwdstaging.co.uk/api/generate')
                    .then((response) => {
                        this.chords = response.data.chords;
                        this.cgkey = response.data.key;
                    });
        },
        methods: {
            onChordsGenerated: function(cgData){
                this.chords = cgData.chords;
                this.cgkey = cgData.key;
            }
        },
        data () {
            return {
                chords: [],
                cgkey: ''
            }
        }
    }

</script>

<style>

</style>
