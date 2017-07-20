# SignInActivity 登入註冊頁面

### 功能與流程簡述：
本頁面讓使用者能透過手機號碼登入或註冊帳號，並且離開本頁面時，會回傳是否登入成功。<br />
註冊與登入是相同的流程，只是兩個功能做在不同的按鈕上。<br />
使用者按下登入或註冊鈕後，要進一步輸入驗證碼，送出驗證碼且server回傳正確，才算是成功登入。<br />
註冊成功後，請自動登入。<br />

##

### 需求列表
| 編號 | 內容 | 新增日期 |
| --- | --- | --- |
| 1 | server驗證碼指定回傳 000000 | 2017/7/19 |

## 

### 程式流程
| 步驟 | 內容 | 附註 |
| --- | --- | --- |
| 1-0 | 判斷local是否有存**登入token**，若有則跳登入成功流程*loginSuccessProcess*，若無則等候使用者選擇登入或註冊。 |  |
| 1-1 | 使用者按下登入或註冊，送出電話號碼*signin_start*，response 409 或 201 代表成功，若成功則要求server重發驗證碼*requestVerifyCode_start*；若失敗則顯示錯誤視窗。 |  |
| 1-2 | 向server要求驗證碼*requestVerifyCode_start*，response 202 代表成功，若成功則等候使用者輸入驗證碼；若失敗則顯示錯誤視窗。 |  |
| 1-3 | 使用者送出驗證碼*sendVerifyCode_start*，response 200 代表成功，若成功則進入*loginSuccessProcess*；若失敗則顯示錯誤視窗。 |  |
| 1-4 | 上述步驟成功則進入*loginSuccessProcess*，結束本頁面並回傳成功訊息。 |  |
| 2-0 | 直接按下返回鍵，則結束本頁面並回傳無操作訊息。 |  |

##

### 程式必要method
| method名稱 | 註解 |
| --- | --- |
| signin_start | 送出電話號碼 |
| requestVerifyCode_start | 要求發驗證碼 |
| sendVerifyCode_start | 送出驗證碼並驗證帳號 |
| loginSuccessProcess | 登入成功後，設定成功訊息並離開本頁面 |
