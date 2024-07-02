## 1. First quark

1. 安裝 quarkus-cli 建立專案
```bash
choco install quarkus
quarkus version
quarkus creat app io.wyziwyz:first-quark --extension='rest' --gradle
cd first-quark
```
   - `--no-code` 快速生成專案基本架構跟配置，但不包含任何預先生成的程式碼
   - `--gradle` 使用 gradle，如果不加，預設是 maven (pom.xml)

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

7. `@Inject` 與 `@ApplicationScoped` 的使用

8. 啟動專案的指令外加 `-Dbebug=false` 或 `-Dsuspend`:

   - `-Dsuspend`:
   - `-Dbebug=false`: 關閉 debug mode

9. `@QuarkusTest`, `@Test` 單元測試

   - dependencies
     ```gradle
     testImplementation 'io.quarkus:quarkus-junit5'
     testImplementation 'io.rest-assured:rest-assured'
     ```
   - 測試使用的框架是 [RestAssured](https://rest-assured.io/)

## 2. OIDC & KeyCloak

1. 可以直接在原有專案加入 oidc 跟 KeyCloak extensions
   ```bash
   quarkus extension add oidc,keycloak-authorization
   ```
   會在 build.gradle 加入這兩個 dependencies
   ```gradle
   implementation 'io.quarkus:quarkus-keycloak-authorization'
   implementation 'io.quarkus:quarkus-oidc'
   ```

2. 實作 UsersResource 跟 AdminResource 類別
   - `@NoCache` 與 `@Authenticated` 標註型別

3. 配置 application.properties
   - `%prod.`