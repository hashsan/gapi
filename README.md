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

### get summary
```js
await api.summary('hogehoge.txt')
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


