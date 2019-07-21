<template>
    <div class="here-map">
        <div ref="map" style="width: 75%; height: 600px"></div>
    </div>
</template>

<script>
    export default {
        name: "HereMap",
        data() {
            return {
                platform: {},
                map: {}
            };
        },
        props: {
            appId: String,
            appCode: String
        },
        mounted() {
            this.platform = new H.service.Platform({
                app_id: this.appId,
                app_code: this.appCode,
            });
            var layers = this.platform.createDefaultLayers();
            this.map = new H.Map(
                this.$refs.map,
                layers.normal.map,
                {
                    center: {lat: "37.7396", lng: "-121.4252"},
                    zoom: 14,
                }
            );
            var events = new H.mapevents.MapEvents(this.map);
            var behavior = new H.mapevents.Behavior(events);
            var ui = H.ui.UI.createDefault(this.map, layers);
        }
    }
</script>

<style scoped></style>
