# gapi
gapi.js is upload to the github repository

```js
var api = gapi(url,ghp)
//ghp is access token. ex) ghp_xxxxxxxxxxxxxxxxxxxxx
```

```js
import "//hashsan.github.io/gapi/gapi.js";

///
var done = document.createElement('button')
done.innerText = 'done'
done.id = 'done'
document.body.append(done)
document.getElementById('done').onclick = load
///

async function load(){
  
  var url ="https://hashsan.github.io/hnikki"
  var ghp = localStorage.getItem('ghp')
  var api = gapi(url,ghp) //<---------------------------------------
  
  //get summary
  var el = document.createElement('pre')
  var res = await api.summary('dev3.txt')
  el.innerHTML=JSON.stringify(res,null,'\n')
  document.body.append(el)
  
  //upload 
  var text ='＃あいうえをこれはテスト'
  var file ='test.txt'
  var res = await api.put(text,file)
  //console.log(res)
  
  //get data
  var da = await api.data(file)
  el.innerHTML=da
}
```

### get list and filter .txt
```js
  var api = gapi(url,auth)
  var res = await api.get()
  console.log(res)
  var list = res.map(d=>d.name)
   .filter(d=>/\.txt/.test(d))
  ;
  console.log(list)
  //["dev.txt","dev1.txt","dev2.txt","dev3.txt","help.txt","test.txt"]

```


### get summary
```js
await api.summary('hogehoge.txt')
```
```
{
    "name": "test.txt",
    "sha": "f22739e3a1efd7821576630dee37e346158d8f44",
    "content": "＃あいうえをこれはテスト",
    "download_url": "https://raw.githubusercontent.com/hashsan/hnikki/main/test.txt",
    "date": "2023-11-07T04:53:54Z",
    "timestamp": 1699332834000,
    "lines": 0,
    "title": "＃あいうえをこれはテスト",
    "time": "2023-11-07 13:53:54",
    "order": "1699332"
}
```

### get data
```js
await api.data('hogehoge.txt')
```

### upload file. create or update. both use.
- first param is data
- __second param is filename__
```js
await api.put('＃データ。これはデータ。データ','hogehoge.txt')
```


### checkAuth standalone
```js
async function checkAuth(token){
  const url = 'https://api.github.com/user'
  const accept = "application/vnd.github.v3+json"  
  const authorization ='token '+ token
  const method ='GET'
  const headers = { 
    accept,
    authorization
  }
  var flg = false
  await fetch(url,{method,headers})
    .then(res=>{
    if(!res.ok) throw new Error('authorization false')
    flg = true
  }).catch(e=>{
    flg =false
    console.log(e)
  })
  //console.log(Config)
  return flg
}  
```


