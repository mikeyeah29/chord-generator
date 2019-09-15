<template>
	<div class="chord-form">
        <div class="d-flex">
            <div class="chord-form__item mr-3">
                <label>Key</label>
                <select class="form-control" v-model="chordprog.cgkey">
                    <option v-for="cgkey in cgkeys" :value="cgkey">{{ cgkey }}</option>
                </select>
            </div>
            <div class="chord-form__item mr-3">
                <label>Scale</label>
                <select class="form-control" v-model="chordprog.scale">
                    <option v-for="scale in scales" :value="scale">{{ scale }}</option>
                </select>
            </div>
            <div class="chord-form__item">
                <label>Bars</label>
                <select class="form-control" v-model="chordprog.bars">
                    <option v-for="bar in bars" :value="bar">{{ bar }}</option>
                </select>
            </div>
        </div>
        <div class="btn btn-primary" @click="getChords">Generate</div>
    </div>
</template>

<script type="text/javascript">
	
	export default {
		methods: {
			getChords: function(){
				var query = '?bars=' + this.chordprog.bars;
				axios.get('http://chordgenapi.rwdstaging.co.uk/api/generate' + query)
                    .then((response) => {
                    	this.$emit('chordsGenerated', response.data);
                        // this.chordprog.chords = response.data.chords;
                        // this.chordprog.cgkey = response.data.key;
                    });
			}
		},
        data () {
            return {
            	chordprog: {
            		cgkey: 'Any',
	                scale: 'Any',
	                bars: 4
            	},
                cgkeys: ['Any', 'C', 'G', 'D', 'A', 'E'],
                scales: ['Any', 'Major', 'Minor'],
                bars: [4, 8, 16]
            }
        }
    }

</script>