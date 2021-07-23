<template>
    <div>
        <div ref="pieChart" style="width: 100%; height: 300px;"></div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                chartInstance: null,
                option: {}
            }
        },
        mounted() {
            this.initChart()
            this.updateChart()
            window.addEventListener('resize', this.handleResize)
        },
        methods: {
            initChart () {
                this.chartInstance = this.$echarts.init(this.$refs.pieChart)
            },
            updateChart () {
                this.option = {
                    xAxis: {
                        type: 'category',
                        data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
                    },
                    yAxis: {
                        type: 'value'
                    },
                    series: [{
                        data: [120, 200, 150, 80, 70, 110, 130],
                        type: 'bar',
                        showBackground: true,
                        backgroundStyle: {
                            color: 'rgba(180, 180, 180, 0.2)'
                        }
                    }]
                }
                this.chartInstance.setOption(this.option)
            },
            // 当浏览器大小发生变化会调用该方法，完成屏幕适配
            handleResize () {
                this.chartInstance && this.chartInstance.resize()
            }
        },
        beforeDestroy() {
            this.chartInstance && this.chartInstance.dispose()
            this.chartInstance = null
            window.removeEventListener('resize', this.handleResize)
        }
    }
</script>

<style lang="">

</style>