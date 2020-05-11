# savml-registry

registry for savml

## savml 工具私服搭建

- 使用 vo-verdaccio 作为私服仓库
- 使用 vo-unpkg 作为私服文件浏览和
- 使用 savml-contract-view 作为合约查看工具

## 安装

```
npm i -g vo-verdaccio vo-unpkg savml-contract-view
npm i -g pm2
```

## 配置启动使用pm2

pm2 配置文件 pm2.yml

 ```yml
 apps:
  - script: verdaccio
    name: vo-verdaccio
    env:
      NPM_CONFIG_REGISTRY: 'http://localhost:4873/'
      UNPKG_URL: '//localhost:4874'
      CONTRACT_URL: '//localhost:4875'
      PORT: 4873
  - script: unpkg
    name: vo-unpkg
    env:
      NPM_REGISTRY_URL: 'http://localhost:4873'
      NODE_ENV: production
      PORT: 4874
  - script: scv
    name: savml-contract-view
    env:
      UNPKG_URL: '//localhost:4874'
      VERDACCIO_URL: '//localhost:4873'
      PKG_PREFIX: 'com.'
      PORT: 4875
 ```
 
 其中 com.是合约包名的前缀，需要酌情修改, 另外这是本地配置， 如果要提供外部访问，需要把localhost等替换为相应地址
 
 pm2 启动命令
 
 ```
 pm2 start pm2.yml
 ```
 
 ## 访问
 
 ```
 http://localhost:4873  npm私服地址
 http://localhost:4874  unpkg地址
 http://localhost:4875  合约查看地址
 ```
 
