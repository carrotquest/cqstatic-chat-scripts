Данный репозиторий содержит в себе скрипт устанавливающийся на клиентском сайте и используется в случаях когда есть необходимость размещать js файлы на своем хостинге и контролировать обновления в ручном режиме.

### Важно
Сборка предусматривает хостинг только js файлов, остальные статичные файлы (изображения, шрифты и пр.) будут использоваться из cdn.carrotquest.app.

### Обратная совместимость.
Данный скрипт может утратить обратную совместимость, поддержка старой версии осуществляется на протяжении двух месяцев.

### Для установки скрипта на хостинг необходимо:

1. Модифицировать установочный код:
```
<!-- Carrot quest BEGIN -->
  <script type='text/javascript'>
	  !function() {
		  function t(t, e) {
			  return function() {
				  window.carrotquestasync.push(t, arguments);
			  };
		  }

		  if ('undefined' == typeof carrotquest) {
			  var e = document.createElement('script');
			  e.type = 'text/javascript', 
            e.async = !0, 
            e.src = '{{CDN_URL}}/api-single.min.js', 
            document.getElementsByTagName('head')[0].appendChild(e), 
            window.carrotquest = {}, window.carrotquestasync = [], carrotquest.settings = {};
			  for (var n = ['connect', 'track', 'identify', 'auth', 'onReady', 'addCallback', 'removeCallback', 'trackMessageInteraction'], a = 0; a < n.length; a++) carrotquest[n[a]] = t(n[a]);
		  }
	  }(), carrotquest.connect('{{API_KEY}}');
  </script>
  <!-- Carrot quest END -->
```
* Вместо **CDN_URL** указать путь до места где храниться файл `api-single.min.js`
* Вместо **API_KEY** указать ваш API Key, его можно найти в разделе `Найстройки > Разработчикам`.

2. Модифицировать содержимое файла `api-single.min.js`:
```
"use strict";/*!
Build date: Thu Aug 29 2024 13:07:15 GMT+0500 (Yekaterinburg Standard Time)
*/function createProxyIframe(){let iframe=document.createElement("iframe");iframe.setAttribute("id","proxy-iframe"),iframe.setAttribute("name","proxy-iframe"),iframe.setAttribute("style","display: block !important; width: 0 !important; height: 0 !important; border: none !important; position: absolute !important; top: 0 !important; left: 0 !important; visibility: hidden !important;"),iframe.addEventListener("load",function(){createScriptIframe()},{once:!0}),document.body.appendChild(iframe);function createScriptIframe(){let indexScript=document.createElement("script");indexScript.type="text/javascript",indexScript.async=!0;
let src="{{CDN_URL}}/index-single.js";indexScript.src=src,indexScript.type="module";let proxyIframe=document.getElementById("proxy-iframe").contentWindow;proxyIframe.document.head.appendChild(indexScript),proxyIframe.parent.dashlyExecuteEval=code=>{eval(code)}}}createProxyIframe();
```
* Вместо **CDN_URL** указать путь до места где храниться файл `index-single.js`

