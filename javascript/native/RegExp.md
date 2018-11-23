# 正则

```js 
name = '*'.repeat(name.length - 1) + name.substring(name.length - 1);
/^\d{1,6}$/.test(string)
/^1[34578]\d{9}$/g.test(phone)
let data = {param: JSON.stringify({url: location.href.split('#')[0]})}

if (window.location.href.indexOf('?') > -1) {
    let urlstr =
    '{"' +
    location.href
        .split('?')[1]
        .split('#')[0]
        .replace(/&/g, '","')
        .replace(/=/g, '":"') +
    '"}'
    let urlObj = JSON.parse(urlstr)
    code = urlObj['code']
}


  if (window.location.href.indexOf('?') > -1) {
    let urlstr = '{"' + decodeURI(window.location.href.replace(/#/ig, '').split('?')[1].split('/')[0].replace(/=/ig, '":"').replace(/&/ig, '","')) + '"}'
    let urlObj = JSON.parse(urlstr)
    code = urlObj['code']
  }

```