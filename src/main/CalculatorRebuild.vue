<template>
    <div class="calculator">
        <Display :value="displayValue" />
        <Button label="AC" @setFunction="clearMemory" triple />
        <Button label="/"  @setFunction="setOperation" operation />
        <Button label="7"  @setFunction="addDigit" />
        <Button label="8"  @setFunction="addDigit" />
        <Button label="9"  @setFunction="addDigit" />
        <Button label="*"  @setFunction="setOperation" operation />
        <Button label="4"  @setFunction="addDigit" />
        <Button label="5"  @setFunction="addDigit" />
        <Button label="6"  @setFunction="addDigit" />
        <Button label="-"  @setFunction="setOperation" operation />
        <Button label="1"  @setFunction="addDigit" />
        <Button label="2"  @setFunction="addDigit" />
        <Button label="3"  @setFunction="addDigit" />
        <Button label="+"  @setFunction="setOperation" operation />
        <Button label="0"  @setFunction="addDigit" double />
        <Button label="."  @setFunction="addDigit" />
        <Button label="="  @setFunction="setOperation" operation/>
    </div>
</template>

<script>
    import Button from '../components/ButtonRebuild';
    import Display from '../components/DisplayRebuild';
export default {
    data() {
        return {
                displayValue: "0",
                clearDisplay: false,
                operation: null,
                values: [0, 0],
                current: 0
            }
    },
    components: { Button, Display },
    methods: {
        clearMemory() {
            Object.assign(this.$data, this.$options.data())
        },
        addDigit(n) {
            if(n === "." && this.displayValue.includes(".")) {
                return
            }

            const clearDisplay = this.displayValue === "0" || this.clearDisplay
            const currentValue = clearDisplay ? "" : this.displayValue
            const displayValue = currentValue + n

            this.displayValue = displayValue
            this.clearDisplay = false
            this.values[this.current] = displayValue
        },
        setOperation(operation) {
            if(this.current === 0) {
                this.operation = operation
                this.current = 1
                this.clearDisplay = true
            } else {
                const equals = operation === "="
                const currentOperation = this.operation

                try {
                    this.values[0] = eval(`${this.values[0]}${currentOperation}${this.values[1]}`)
                } catch (e) {
                    this.$emit('onError', e)
                }

                this.values[1] = 0
                this.displayValue = this.values[0]
                this.operation = equals ? null : operation
                this.current = equals ? 0 : 1
                this.clearDisplay = !equals
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
    overflow: hidden;

    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-auto-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>