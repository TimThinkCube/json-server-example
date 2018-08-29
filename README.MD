# JSON Server 使用說明書

## 安裝 json Server
```
  $ npm install json-server -s
```
## 啟動 json Server
```
  $ mkdir json-server
  $ cd json-server
  $ json-server db.json
```
1. 建置一個假 server資料夾存放資料庫位置，並進入
2. 啟動 json-Server ，此時於資料夾中會產生一個 json-Server 指定的資料庫檔案 db.json
3. 打開 db.json 提供三種預設資料 posts、comments、profiles，每個 field 相當於一個資料表(table)，可以自行修改 JSON 建立假資料。
4. json-Server 預設的 port 會架設於 3000，於瀏覽器中打開 http://localhost:3000 ，提供三種預設的table 可取得的資料。
			- http://localhost:3000/posts
			- http://localhost:3000/comments
			- http://localhost:3000/profile
5. 可以使用 postman 測試，也可以用ajax、axios、fetch...etc
6. JSON Server 支援開發中最常用的 GET、POST、PUT、PATCH 與 DELETE。

  - GET
    - 選擇方法 GET 
    - 填入服務網址 http://localhost:3000/posts
    - Send
 			![GET](https://i.imgur.com/837GE3A.png)
				
  - POST
    - 選擇方法 POST  
    - 填入服務網址 http://localhost:3000/posts
    - 新增資料 → Body → raw → format: JSON(application/json)
    
		```
		{
		  "title": "post data",
		  "author": "timwu"
		}
		```
    - Send
				![POST](https://i.imgur.com/l0OPOun.png)
				
  - PUT
    - 選擇方法 POST  
    - 服務網址 http://localhost:3000/posts/2
    - 更新資料 → Body → raw → format: JSON(application/json)
    - 使用上需要與 PATCH 做區別，透過 PUT 進行資料更新會覆蓋掉整個物件
    
		```
		{
		  "title": "data update",
		  "author": "timwu"
		}
		```
    - Send
   	![PUT](https://i.imgur.com/NquSkK4.png) 
				
  - PATCH
    - 選擇方法 PATCH  
    - 服務網址 http://localhost:3000/posts/2
    - 更新資料 → Body → raw → format: JSON(application/json)
    - 使用上需要與 PUT 做區別，PATCH 只會更新符合的資料
    
		```
		{
		  "title": "data update"  
		}
		```
    - Send
    ![PATCH](https://i.imgur.com/he5sCAg.png)
  - DELETE
    - 選擇方法 DELETE  
    - 服務網址 http://localhost:3000/posts/2
    - Send
    - 會直接刪除posts/:id 下符合的資料
				![DELETE](https://i.imgur.com/luXX7Sr.png)
## 自訂路由
在專案開發上，我們常會透過不同的路由帶不同的參數來取得資料，這時候我們可以透過自訂路由的方式來模擬，作法如下
1. 先建立一個 routes.json 來客製化路由。
2. 設定路由內容，這邊的範例是將預設的路由改為，我們指定的路由，設定如下：
```
{
  "/testapi/posts": "/posts",
  "/testapi/posts/:id": "/posts/:id"
}
```
這個設定做了兩件事，一種是將原本的 "/posts" 的路由改為 "/testapi/posts"，另一個則是將 "/posts/:id" 改為 "/testapi/posts/:id"
3. 啟用修改路由後的 db ，啟動的方法同上，但是需要新增 " --routes routes.json " 在原本的指令後方來套用路由的設定
```
 json-server db.json --routes routes.json
```

4. posts 的資料現在可以透過 http://localhost:3000/testapi/posts 也可以透過 http://localhost:3000/posts 存取
![custom-route-api](https://i.imgur.com/kgG7BiR.png)
## 備份資料庫
在更動資料時，難免會有誤刪、誤植的情況，json-server 也提供了像資料庫一樣做 snapshot 的功能，只需要在終端機按下
```
  S + enter
``` 
此時在你的資料庫存放資料夾會產生一個亂數序列的備份檔案 e.g: db-1535532923118.json，這個json 檔案的資料會與 db.json 相同！

## 參考資料
[json-Server 文件](https://github.com/typicode/json-server)
