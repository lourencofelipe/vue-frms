<template>
    <div>
        <label>{{ customLabel }}</label>
        <input 
        type="range"
        v-bind="$attrs"
        :value="value"
        :class="inputClasses"
        @input="atualizar"> 
    </div> 
</template>
<script>
export default {
    // Os atributos que forem passados para dentro do componente que não possuir uma prop definida não serão colocados no elemento root
    inheritAttrs: false,
    props: {
        label: String,
        value: [Number, String],
        inputClasses: [String, Object, Array]
    },
    data() {
        return {
            valorAtual: this.value || this.$attrs.min
        }
    },
    computed: {
        customLabel() {
            return `${this.label} (R$ ${this.valorAtual})`
        }
    },
    methods: {
        atualizar(event) {
            // Recebe valor atual do input
            const valor = event.target.value
            // Emite um evento do tipo input e é passado como valor o que vier na constante.
            this.$emit('input', valor)
            this.valorAtual = valor
        }
    },
    created() {
        console.log('Attrs:', this.$attrs)
    }
}
</script>