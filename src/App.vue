<script setup lang="ts">
import {onLaunch, onShow, onHide} from '@dcloudio/uni-app'

onLaunch(() => {
    console.log('App Launch1')
})
onShow(() => {
    console.log('App Show')
})
onHide(() => {
    console.log('App Hide')
})
</script>
<style></style>
