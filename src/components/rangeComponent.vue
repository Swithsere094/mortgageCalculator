<script>
    import {ref} from 'vue';

    export default {
        name: "rangeComponent",
        props: {
            subtitle: String,
            min: String,
            max: String,
            type: String,
        },
        setup(props) {
            const value = ref(props.min)
            const types = {
                1 : '$',
                2 : 'years',
                3 : '%'
            }
            return {
                types,
                value,
            };
        },
        methods: {
            emitOnChange(selectedValue) {
                this.$emit('changeValue', {
                                            "selectedValue": selectedValue.target.value,
                                            "type": this.subtitle.split(" ")[0]
                                        }
                            )
            }
        }
    }
</script>

<template>
    <div>
        <h2>{{ subtitle }} <strong>{{ value }} {{ types[type] }}</strong></h2>
        <input :min=min :max=max type="range" v-model="value" v-on:change="emitOnChange">
    </div>
</template>

<style scoped>
    h2 {
        font-weight:600;
    }

    input[type=range] {
        height: 39px;
        -webkit-appearance: none;
        appearance: none;
        background: transparent;
        margin: 10px 0;
        width: 100%;
    }
    input[type=range]:focus {
        outline: none;
    }
    input[type=range]::-webkit-slider-runnable-track {
        width: 100%;
        height: 12px;
        cursor: pointer;
        box-shadow: 2px 2px 2px #6B549C;
        background: #AF89FF;
        border-radius: 4px;
        border: 0px solid #8064BA;
    }
    input[type=range]::-webkit-slider-thumb {
        box-shadow: 1px 1px 2px #584580;
        border: 4px solid #8265BD;
        height: 28px;
        width: 28px;
        border-radius: 10px;
        background: #AF89FF;
        cursor: pointer;
        -webkit-appearance: none;
        margin-top: -10px;
    }
    input[type=range]:focus::-webkit-slider-runnable-track {
        background: #AF89FF;
    }
    input[type=range]::-moz-range-track {
        width: 100%;
        height: 12px;
        cursor: pointer;
        box-shadow: 2px 2px 2px #6B549C;
        background: #AF89FF;
        border-radius: 4px;
        border: 0px solid #8064BA;
    }
    input[type=range]::-moz-range-thumb {
        box-shadow: 1px 1px 2px #584580;
        border: 4px solid #8265BD;
        height: 28px;
        width: 28px;
        border-radius: 10px;
        background: #AF89FF;
        cursor: pointer;
    }
    input[type=range]::-ms-track {
        width: 100%;
        height: 12px;
        cursor: pointer;
        background: transparent;
        border-color: transparent;
        color: transparent;
    }
    input[type=range]::-ms-fill-lower {
        background: #AF89FF;
        border: 0px solid #8064BA;
        border-radius: 8px;
        box-shadow: 2px 2px 2px #6B549C;
    }
    input[type=range]::-ms-fill-upper {
        background: #AF89FF;
        border: 0px solid #8064BA;
        border-radius: 8px;
        box-shadow: 2px 2px 2px #6B549C;
    }
    input[type=range]::-ms-thumb {
        margin-top: 1px;
        box-shadow: 1px 1px 2px #584580;
        border: 4px solid #8265BD;
        height: 28px;
        width: 28px;
        border-radius: 10px;
        background: #AF89FF;
        cursor: pointer;
    }
    input[type=range]:focus::-ms-fill-lower {
        background: #AF89FF;
    }
    input[type=range]:focus::-ms-fill-upper {
        background: #AF89FF;
    }


</style>