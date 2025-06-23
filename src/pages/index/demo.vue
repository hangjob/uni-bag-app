<template>
    <div>
        <button @click="getTest">GET 请求</button>
        <button @click="postTest">POST 请求</button>
        <button @click="cancelRequest">取消 请求</button>
        <button @click="awaitToJs">awaitToJs</button>
        <wd-button>主要按钮</wd-button>
        <wd-button type="success">成功按钮</wd-button>
        <wd-button type="info">信息按钮</wd-button>
        <wd-button type="warning">警告按钮</wd-button>
        <wd-button type="error">危险按钮</wd-button>
        <wd-signature @confirm="confirm" @clear="clear" :export-scale="2" background-color="#ffffff"/>
        <wd-cell title="默认键盘" is-link @click="showKeyBoard" />
        <wd-toast />
        <wd-number-keyboard v-model:visible="visible" @input="onInput" @delete="onDelete"></wd-number-keyboard>
    </div>
</template>

<script setup lang="ts">
import {awaitToJsTestApi, getTestApi, postTestApi} from '@/api/testApi'
import { useToast } from 'wot-design-uni'
// GET 请求
const getTest = async () => {
    const res = await getTestApi({name: 'uni-lin'})
    console.log(res)
}

// POST 请求
let requestTask = null
const postTest = () => {
    requestTask = postTestApi({name: 'uni-lin'}, {id: '123456'})
    requestTask
        .then(res => {
            console.log(res)
        })
        .catch(err => {
            console.log(err)
        })
}

// 取消 请求
const cancelRequest = () => {
    // 取消请求
    requestTask.abort()
}

/* await-to-js 代替 try catch 用法，根据实际需求进行使用 */
const awaitToJs = async () => {
    const [data, err] = await awaitToJsTestApi({name: 'uni-lin'})
    if (data) {
        console.log(data)
    }
    if (err) {
        console.log(err)
    }
}

const img = ref({})

function confirm(result) {
    if (result.success) {
        uni.previewImage({
            urls: [result.tempFilePath]
        })
    }
}

function clear() {
    img.value = {}
}

const { show: showToast } = useToast()
const visible = ref<boolean>(false)

function showKeyBoard() {
    visible.value = true
}

const onInput = (value) => showToast(`${value}`)
const onDelete = () => showToast('删除')
</script>
