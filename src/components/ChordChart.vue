<template>
	<div class="chord-chart">

		<h2>Key: {{ cgkey }} Major</h2>
        <div class="row">
            <div class="col-sm-3" v-for="chord in chords">
                <chord>{{ chord.name }}</chord>
            </div>
        </div>

    </div>
</template>

<script type="text/javascript">
	
	import Chord from './Chord.vue';

	export default {
		props: ['chords', 'cgkey'],
		components: {
			Chord
		},
        data () {
            return {
                
            }
        }
    }

</script>