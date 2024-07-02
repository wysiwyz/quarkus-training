## 1. First quark

1. 安裝 quarkus-cli 建立專案
```bash
choco install quarkus
quarkus version
quarkus creat app io.wyziwyz:first-quark --extension='rest' --gradle
cd first-quark
```

2. Quarkus BOM, or an enforcedPlatform directive for the Quarkus BOM
   - 允許你忽略不同 Quarkus dependencies 的版本

3. Run 看看專案
```bash
./gradlew --console=plain quarkusDev
```

![console](https://hackmd.io/_uploads/BkP0eQbwC.png)

4. Start 完了可以發送請求給 endpoint
   ```bash
   curl -w "\n" http://localhost:8080/hello
   ```
   - `-w`, `--write-out` 用來在output結尾加上一個換行符號

5. 另外 Quarkus 有 Live reload 不用改了程式就還要再重新 rerun 專案
   ![live-reload](https://hackmd.io/_uploads/r1IzQX-vC.png)

6. Quarkus 的依賴注入是基於 ArC，這是根據 Quarkus 架構所量身訂做的 CDI-based 依賴注入解決方案
   - ArC: 基於CDI，優化性能跟啟動時間，若要使用的話要加 dependency `quarkus-rest`
   - CDI: JavaEE 標準的依賴注入規範，參考[Intro to CDI](https://quarkus.io/guides/cdi))