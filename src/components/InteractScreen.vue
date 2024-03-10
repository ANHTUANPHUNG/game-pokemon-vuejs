<template>
    <div class="container__render__card" >
        <div class="screen" :style="{ width: `${getWidthColumns()}px` }">
        <card-product 
        v-for="(card, index) in cardsContext " 
        :key="index"
        :ref ="`card-${index}`"
        :imgBack="`images/${card}.png`"
        :card = "{index : index, value: card}"
        @onFlip="checkRule($event)"

        />
    </div>
    </div>
</template>

<script>
import CardProduct from "./CardProduct.vue";
export default {
    props: {
        cardsContext: {
            type: Array,
            default: function (){
                return [];
            }
        }
    },
    components: {
        CardProduct,
    },
    data() {
        return {
            rules: [],
        }
    },
    methods:{
        checkRule(card) {
            if(this.rules.length === 2 ) return false;
            this.rules.push(card);
            if(this.rules.length === 2 && this.rules[0].value === this.rules[1].value){
                this.$refs[`card-${this.rules[0].index}`][0].onEnabled();
                this.$refs[`card-${this.rules[1].index}`][0].onEnabled();
                this.rules = []
                const disabledElements = document.querySelectorAll(".screen .card.disabled")
                if(disabledElements && disabledElements.length === this.cardsContext.length -2){
                    setTimeout(()=>{
                        this.$emit("onFinish")
                    }, 800)
                }
            }  else if (
                this.rules.length === 2 &&
                this.rules[0].value !== this.rules[1].value
            ) {
            setTimeout(() => {
                this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
                this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
                this.rules = [];
            }, 800);
            } else return false;          
        },
        getWidthColumns() {
      const columns = Math.sqrt(this.cardsContext.length)*106;
      return columns ;
    },
        getHeightColumns() {
      const columns = Math.sqrt(this.cardsContext.length)*137;
      console.log(columns);
      return columns ;
    },

    }
}
</script>   
<style lang="css" scoped>
    .screen {
        display: flex;
        flex-wrap: wrap;
    }
    .container__render__card{
        background-color: #212121;
        display: flex;
        justify-content: center;
        padding: 60px 0;
    }
</style>