<template>
    <div>
    </div>
</template>

<script>
import webgazer from "webgazer";
    export default {
        name: "WebGazer",
        props: {
            off: {
                type: Boolean,
                default: false,
            },
        },

        data : function(){
            return {
                x: 0,
                y: 0,
            };
        },
        async created() {
            if (window && !this.off) {
                const thiz = this;
                window.applyCalmanFilter = true;
                window.saveDataAccrossSessions = true;
                webgazer.params.showVideoPreview = false;
                await webgazer
                    .setRegression("ridge")
                     .setGazeListener(function(data, elapsedTime) {

                         console.log(elapsedTime);

                         if (data) {
                             thiz.x = data.x;
                             thiz.y = data.y;
                             thiz.$emit("update", { x: data.x, y: data.y });
                         }
                     })
                    .begin();
                    //var prediction = webgazer.getCurrentPrediction();
                    //if (prediction) {
                    //    thiz.x = prediction.x;
                    //    thiz.y = prediction.y;
                    //    thiz.$emit("update", { x: prediction.x, y: prediction.y });
                    //}
                webgazer.showPredictionPoints(true);
            }
        },
        beforeDestroy() {
            webgazer.end();
        },
        // var prediction = webgazer.getCurrentPrediction();
        // if (prediction) {
        //     var x = prediction.x;
        //     var y = prediction.y;
        // };
    }
</script>

<style lang="scss" scoped>

</style>