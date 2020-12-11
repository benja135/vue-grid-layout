<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "Resizable",
    props: {
        rowHeight : {
            type: Number,
            default: 30
        }
    },

    data: function() {
        return {
            clientHeight: 0,
            widgetHeight: 0,
            gridItem: null
        }
    },

    mounted() {
        this.gridItem = this.$parent

        const widgetHeight = this.$el.clientHeight
        const newHeight = Math.ceil((widgetHeight + this.gridItem.margin[1]) / (this.rowHeight+ this.gridItem.margin[1]))

        if (widgetHeight !== this.widgetHeight) {
            this.widgetHeight = widgetHeight

            this.gridItem.eventBus.$emit(
                'resizeEvent',
                'resizeend',
                this.gridItem.i,
                this.gridItem.x,
                this.gridItem.y,
                newHeight,
                this.gridItem.w,
            )
        }
    }
}
</script>
