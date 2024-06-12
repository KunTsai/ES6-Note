# js處理等待
* 同步事件
  * 一次可以同時做很多事，不需要等待前一件事完成
 
* 非同步事件
  * 一次做一件事，逐步處理
  * 需要非同步事件的理由是:如果全都同步執行的話，會造成阻塞(Blocking)，阻塞是一種現象，因為上一件事還沒完成，所以下一件事不會進行，網頁就會像當掉一樣。
  * 非同步方法舉例:
    * 向 API 發送請求：如果不使用非同步執行，那呼叫一支 API，在等待資料回傳的過程中，網頁沒辦法執行或渲染，只能等。
    * 使用setTimeout()模擬非同步狀況，得出先擱置任務B進入任務C，再回頭處理任務B，最後做總回報。
      ```CSS
      (() => {
      console.log('任務A');
       })();
      setTimeout(() => {
      console.log('任務B');
      }, 1000);
      (() => {
      console.log('任務C');
      })();
      ```
    * querySelector()
      ```CSS
      const btn = document.querySelector("button");
      btn.addEventListener("click", () => {
      alert("你點擊了我！");

      let pElem = document.createElement("p");
      pElem.textContent = "這是一段新加的文字。";
      document.body.appendChild(pElem);
      });
      ```

* promise
  * promise物件一開始會有以下狀態:
    * 擱置（pending）：初始狀態，不是 fulfilled 與 rejected。
    * 實現（fulfilled）：表示操作完成。
    * 拒絕（rejected）：表示操作失敗。
  * promise建構子語法結構:
    ```CSS
    new Promise((resolve, reject) => {
    statement
    })
    ```
  * 將promise放入function並回傳，這個function就有了promise的功能
    ```CSS
    function asyncFunc(value) {
      return new Promise(function (resolve, reject) {
          if (value)
              resolve(value);
          else
              reject(reason);
      });
    }
  ```
* then
  * 為回傳promise物件並使用then方法來處理promise物件的狀態
    ```CSS
    p.then(onFulfilled, onRejected);
    p.then((response) => {
      // 執行成功
    }, (error) => {
      // 執行失敗
    });
    ```
  * 有兩個參數可用:
    * onFulfilled是當promise物件執行成功，狀態為實現（fulfilled）呼叫的函式，並有一個傳入值(value)做後續的運算。
    * onRejected是當promise物件執行失敗，狀態為拒絕（rejected）呼叫的函式，一樣有一個傳入值(reason)做後續的處理。
    ```CSS
    async ('ABC').then(
      response => {
          console.log(`第1次輸入值：${response}`);
          return async ('DEF');
      }, error => {
          console.log(`錯誤：${error}`);
      }
    ).then(
      response => {
          console.log(`第2次輸入值：${response}`);
      }, error => {
          console.log(`錯誤：${error}`);
      }
    );
    ```
* await
  * Promise 中完成會透過 then 來回傳，在 await 中他則是會等待這段函式完成後在往下繼續執行，是一個卡住的概念。
    ```CSS
    let runPromise = (someone, timer, success = true) => {
    console.log(`${someone} 開始跑開始`);
    return new Promise((resolve, reject) => {
    // 傳入 resolve 與 reject，表示資料成功與失敗
    if (success) {
      setTimeout(function () {
        // 3 秒時間後，透過 resolve 來表示完成
        resolve(`${someone} 跑 ${timer / 1000} 秒時間(fulfilled)`);
      }, timer);
    } else {
      // 回傳失敗
      reject(`${someone} 跌倒失敗(rejected)`)
    }
    });
    }

      // 此段函式並不會影響其它函示的執行
      runPromise('小明', 3000).then(someone => {
      console.log('小明', someone)
      });
      // 以下這段 console 會在 promise 結束前就執行
      console.log('這裡執行了一段 console');

    // 此段函示會中斷其它函式的運行
    let mingRun = await runPromise('小明', 2000)
    console.log('跑完了:', mingRun);
    let auntieRun = await runPromise('漂亮阿姨', 2500);
    console.log('跑完了:', auntieRun);
* async
   * 它的結構非常類似 Promise，只不過他能夠將 await 包在裡面，被包在裡面的 await 就如同先前的結構一樣，他會依序地執行。
   * async 本身也是類似 Promise，在正確執行的情況下 return 會傳回 resolved 的狀態，也可以使用 then 來接收正確的資料。
      ```CSS
      const asyncRun = async () => {
        let mingRun = await runPromise('小明', 2000);
        let auntieRun = await runPromise('漂亮阿姨', 2500);
      return `${mingRun}, ${auntieRun}`
      }
      asyncRun().then(string => {
        console.log(string)
      }).catch(response => {
        console.log(string)
      })

      const asyncRunFail = async () => {
        let mingRun = await runPromise('小明', 2000, false);
        let auntieRun = await runPromise('漂亮阿姨', 2500);
        return `${mingRun}, ${auntieRun}`
      }
      asyncRunFail().then(string => {
        console.log(string);
      }).catch(response => {
        console.log(response);
      // 小明 跌倒失敗(rejected)
      })
      ```
