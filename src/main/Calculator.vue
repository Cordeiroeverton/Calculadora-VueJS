<template>
  <div class="calculator">
      <Display :value="DisplayValue" />
      <Button label="AC" triple @onClick="clearMemory" />
      <Button label="/" operation @onClick="setOperation" />
      <Button label="7" @onClick="addDigit" />
      <Button label="8" @onClick="addDigit"  />
      <Button label="9" @onClick="addDigit" />
      <Button label="*" operation @onClick="setOperation"  />
      <Button label="4" @onClick="addDigit" />
      <Button label="5" @onClick="addDigit" />
      <Button label="6" @onClick="addDigit" />
      <Button label="-" operation @onClick="setOperation"  />
      <Button label="1" @onClick="addDigit" />
      <Button label="2" @onClick="addDigit" />
      <Button label="3" @onClick="addDigit" />
      <Button label="+" operation @onClick="setOperation"  />
      <Button label="0" double @onClick="addDigit" />
      <Button label="." @onClick="addDigit" />
      <Button label="=" operation @onClick="setOperation"  />

  </div>
</template>

<script>
import Button from "../components/Button"
import Display from "../components/Display"

export default {
    data: function() {
        return {
            DisplayValue:"0",
            clearDisplay: false,
            operation: null,
            values: [0, 0],
            current: 0
        }
    },
    components: { Button, Display },
    methods: {
        clearMemory() {
          Object.assign(this.$data, this.$$options.data())
        },
      
        // eslint-disable-next-line no-unused-vars
        setOperation(operation) {
                if(this.current === 0) {
                    this.operation =  operation
                    this.current = 1
                    this.clearDisplay = true
                } else {
                    // eslint-disable-next-line no-unused-vars
                    const equals = operation ===  "="
                    // eslint-disable-next-line no-unused-vars
                    const currentOperation = this.operation
                    try {
                        this.values[0] = eval(
                           `${this.values[0]} ${this.currentOperation} ${this.values[1]}` 
                        )
                    } catch (e) {
                        this.$emit('onError', e)
                    }
                    this.values[1] = 0
                    this.displayValue =  this.values[0]
                    this.operation = equals ? null : operation
                    this.current = equals ? 0 : 1
                    this.clearDisplay = !equals
                }
        },
        addDigit(n) {
            if (n === "." && this.DisplayValue.includes(".")) {
                return
            }
            const clearDisplay = this.DisplayValue == "0" || this.clearDisplay  
            const currentValue = clearDisplay ? "" : this.DisplayValue
            const displayValue = currentValue + n 

            this.displayValue = displayValue 
            this.clearDisplay = false

            if (n !== ".") {
                // eslint-disable-next-line no-unused-vars
                const i = this.current
                // eslint-disable-next-line no-unused-vars
                const newValue = parseFloat(displayValue)
                this.values[i] = newValue
            }
        }
    }
}
</script>

<style>
    .calculator {
        height: 320px;
        width: 235px;
        border-radius: 5px;
        overFlow: hidden;

        display: grid;
        grid-template-columns: repeat(4, 25%);
        grid-template-rows:1fr 48px 48px 48px 48px 48px 48px;
    }
</style>