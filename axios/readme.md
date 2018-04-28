axios封装（未完待续）
-------
~~~
'use strict'

import axios from 'axios'
import qs from 'qs'

axios.interceptors.request.use(config => {
  // loading
  return config
}, error => {
  return Promise.reject(error)
})

axios.interceptors.response.use(response => {
	console.log("返回的拦截器："+response);
  return response
}, error => {
  return Promise.resolve(error.response)
})

function checkStatus (response) {
  // loading
  // 如果http状态码正常，则直接返回数据
  // if (response && (response.data.status === 200 || response.data.status === 304 || response.data.status === 400)) {
  if (response && (response.data.status === 1)) {
    return response
    // 如果不需要除了data之外的数据，可以直接 return response.data
  }
  // 异常状态下，把错误信息返回去
  return {
    status: -404,
    msg: response.data.msg
  }
}

function checkCode (res) {
  // 如果code异常(这里已经包括网络错误，服务器错误，后端抛出的错误)，可以弹出一个错误提示，告诉用户
  if (res.status === -404) {
    console.log("错误信息："+res.msg)
  }
  if (res.data && (!res.data.success)) {
    console.log("错误信息2："+res.data.error_msg)
  }
  return res
}

export default {
  post (url, data) {
    return axios({
      method: 'post',
      baseURL: '/api',
      url,
      data: qs.stringify(data),
      timeout: 10000,
      headers: {
        'X-Requested-With': 'XMLHttpRequest',
        'Content-Type': 'application/x-www-form-urlencoded; charset=UTF-8'
      }
    }).then(
      (response) => {
      	console.log(response);
        return checkStatus(response)
      }
    ).catch(
      (res) => {
        return checkCode(res)
      }
    )
  },
  get (url, params) {
    return axios({
      method: 'get',
      baseURL: '/api',
      url,
      params, // get 请求时带的参数
      timeout: 10000,
      headers: {
        'X-Requested-With': 'XMLHttpRequest'
      }
    }).then(
      (response) => {
        return checkStatus(response)
      }
    ).then(
      (res) => {
        return checkCode(res)
      }
    )
  }
}
~~~

async和await正常使用要安装babel-preset-stage-3（目前vue-cli自带的是babel-preset-stage-2）
封装后使用方法如下：
~~~
//main.js
import axios from './utils/ajax/axios.js'//封装地址

Vue.prototype.$ajax = axios

//使用
fetchData: async function(){
      let params = {
      }
      const res = await this.$ajax.post(url,params)
      console.log(res);
      
    }
~~~
