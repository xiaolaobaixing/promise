# promise
class Promise {
succeed = null
fail = null
state = 'pending'   //(当前状态）
resolve(result) {
  setTimeout(() => {
  this.state = 'fulfiled'
  this.succeed(result) 
   })
  }      //需要resolve时将状态变化，同时执行成功的对应函数，将结果发送
reject(reason) {
  setTimeout(()=> {
  this.state = 'rejected'
  this.fail(reason)
   })
} //,当执行reject时失败将state变为rejected执行fail函数，

constructor（fn) {
 fn(this.resolve.bind(this),this.reject.bind(this))
}

then(succeed,fail){
 this.succeed = succeed
 this.fail = fail
}
}

new Promise((resolve,reject) => {
  console.log('fn run...')
  setTimeout() => {
   if(Math.random() > 0.5) {
     resolve(100)
 } else {
   reject('失败')
  }
 },1000)
}).then(n =>{
  console.log(n)
},reason => {
 console.log(reason)
})




class Promise2 {
  state = 'pending'
  succeed = null
  fail = null
  
  resolve(result) {
    setTimeout(() => {
     this.state = 'fulfilled'
     this.succeed(result)
    })
  }
  
  reject(err) {
    setTimeout(() => {
      this.state = 'rejected'
      this.fail(err)
    })
  }
  
  constructor(fn) {
    fn(this.resolve.bind(this), this.reject.bind(this))
  }

  then(succeed, fail) {
    this.succeed = succeed
    this.fail = fail
  }
}


实列代码部分

const getWeather = city => new Promise2((resolve, reject) => {
  let xhr = new XMLHttpRequest()
  xhr.open('GET', 'http://rap2.taobao.org:38080/app/mock/245421/getWeather?city='+city, true)
  xhr.onload = () => {
    if(xhr.status === 200) {
      resolve(JSON.parse(xhr.responseText))
    } else {
      reject(`获取${city}天气失败`)
    }
  }
  xhr.send()
})

getWeather('北京')
.then(data => {
  console.log(data)
}, err => {
  console.log(err)
})
