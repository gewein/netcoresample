Centos7
netcore 2.2

*サーバー設定
usr/src/netcoresample/ にソースディレクトリを作成
cdを移動し、「$dotnet run」で起動する


**Apacheのリーバースプロキシ
etc/conf/httpd.confに以下を追記する

code(httpd.conf){
  ...
  LoadModule proxy_module modules/mod_proxy.so
  LoadModule proxy_http_module modules/mod_proxy_http.so

  ProxyRequests Off
  ProxyPass /api http://localhost:5000/api

  #よくわからないのでスルー、リダイレクト時の挙動をコントロールするらしい
  #ProxyPassReverse / http://test1.com/ 
...
}


これでapacheで公開しているURL/api～でアクセスすると、「http://localhost:5000」で動いているnetcoreのサーバーにつなげてくれる


