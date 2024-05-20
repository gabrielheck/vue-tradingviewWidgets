<template>
    <div ref="tradingview" :id="container" />
</template>
<script lang="ts">
import { defineComponent } from 'vue'
import useInitWidget from '../composable/useInitWidget'

export default defineComponent({
    name: 'WStockHeatMap',
    props: {
        options: {
            type: Object,
            default: () => ({}),
        },
    },
    setup(props) {
        const options = {
            exchanges: [],
            dataSource: "SPX500",
            grouping: "sector",
            blockSize: "market_cap_basic",
            blockColor: "change",
            locale: "en",
            symbolUrl: "",
            colorTheme: "light",
            hasTopBar: false,
            isDataSetEnabled: false,
            isZoomEnabled: true,
            hasSymbolTooltip: true,
            isMonoSize: false,
            width: "100%",
            height: "100%",
            ...props.options,
        }
        
        const { container, tradingview } = useInitWidget(
            options,
            'tradingview-stock-heat-map',
            'tradingview-stock-heat-map-script',
            'https://s3.tradingview.com/external-embedding/embed-widget-stock-heatmap.js'
        )

        return { container, tradingview }
    },
})
</script>
