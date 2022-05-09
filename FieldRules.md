Field rules of H.E.I.S.
===


[![hackmd-github-sync-badge](https://hackmd.io/NVUn7WAxSIC-swUjXVYIuw/badge)](https://hackmd.io/NVUn7WAxSIC-swUjXVYIuw)
## System Config (FUNC_ID = 'SYS017')
- 設定該虛擬機的測試信件收信Email地址
- 設定虛擬機所在的伺服器IP位置或域名

```
⚠️⚠️⚠️
Server IP Address or Domain(原為Server IP)
和Server Domain欄位重複，是否保留Server Domain欄位？
```

![](https://i.imgur.com/znvTmT8.png)

:::spoiler Test Email Address 測試信收信信箱
| Table | Column | Datatype |
| -------- | -------- | -------- |
| SYS_CODE_INFO | VARCHAR06 | VARCHAR(100) |

#### 檢查規則
- 必填欄位（不可為null、不可為空字串）
:::

:::spoiler Server IP Address or Domain 主程式所在伺服器IP位置或域名
| Table | Column | Datatype |
| -------- | -------- | -------- |3
| SYS_CODE_INFO | VARCHAR01 | VARCHAR(300) |

#### 檢查規則
- 必填欄位（不可為null、不可為空字串）
- 長度為300以下
:::

:::spoiler Server Domain 服務主機域名
| Table | Column | Datatype |
| -------- | -------- | -------- |
| SYS_CODE_INFO | VARCHAR03 | VARCHAR(100) |

#### 檢查規則
無檢查
:::

:::spoiler Email Server IP 郵件主機IP位置
| Table | Column | Datatype |
| -------- | -------- | -------- |
| SYS_CODE_INFO | VARCHAR04 | VARCHAR(100) |

#### 檢查規則
- 以Dot(.)分隔的四組數字 `/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/g`
    - 接受 `1.1.1.01`、`192.168.1.256`
    - 不接受 `1.1.1.1,1.1.1.1`、`-1.2.3.4`、`1.1.1.1.`、`3...3`
:::

:::spoiler Email Server Domain 郵件主機域名
| Table | Column | Datatype |
| -------- | -------- | -------- |
| SYS_CODE_INFO | VARCHAR05 | VARCHAR(100) |

#### 檢查規則
無檢查

:::

## Security (FUNC_ID = 'SYS530')
白名單管理
:::danger
目前沒有阻擋重複內容
:::

:::spoiler 操作步驟
1. 在Whitelist Name輸入對IP自訂名稱
![](https://i.imgur.com/N3t5498.png)
2. 如果想加入白名單的是單一IP地址，可點擊Add IP Address，接著會出現一個輸入欄位
![](https://i.imgur.com/XqlsGFX.png)
3. 如果想加入白名單的是指定範圍的IP地址，可點擊Add IP Range，接著會出現兩個輸入欄位
![](https://i.imgur.com/buVnikq.png)
4. 輸入完成後需點擊Save後，會進行輸入內容的檢查，需符合`/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/g`，才會送至後端程式
5. 最後在資料庫的`MIS_IP`表單中，會儲存成`IP_START`和`IP_END`兩個欄位：
![](https://i.imgur.com/MgkmtYD.png)
:::

![](https://i.imgur.com/i05mgVy.png)

:::spoiler Whitelist Name
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| MIS_IP   | IP_NAME  | VARCHAR(30) |

#### 檢查規則
- 必填欄位（不可為null、不可為空字串）
:::

:::spoiler IP Address 或 IP Range
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| MIS_IP   | IP_START  | VARCHAR(30) |
| MIS_IP   | IP_END  | VARCHAR(30) |

#### 檢查規則
- 必填欄位（不可為null、不可為空字串）
- 以Dot(.)分隔的四組數字 `/[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+/g`
    - 接受 `1.1.1.01`、`192.168.1.256`
    - 不接受 `1.1.1.1,1.1.1.1`、`-1.2.3.4`、`1.1.1.1.`、`3...3`
:::

## Admin Setting (FUNC_ID = 'USR061')
- 管理者清單的顯示和搜尋
- 單一管理者的新增和編輯

:::danger
各頁面欄位名稱不對應

| Admin List | Admin Setting Edit | New Account |
| ---------- | ------------------ | ----------- |
| `ID` | `Account` | `Account` |
| `Name` | `User Name` | `User Name` |

:::
![](https://i.imgur.com/cZfVTxt.png)

#### Admin List 顯示功能
:::spoiler Name 管理者名稱
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_NAME  | VARCHAR(100) |
:::
:::spoiler ID 管理者ID編號
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_ID  | VARCHAR(30) |
:::
:::spoiler Email 管理者電子信箱
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_MAIL  | VARCHAR(50) |
:::
:::spoiler Last Login 管理者最近登入日期時間
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | LAST_LOGIN  | DATETIME |
:::

#### Admin List 搜尋功能
- 針對`Name`、`ID`和`Email`搜尋是否包含該關鍵字
- 欄位可輸入空字串、夾帶空白的字串

### Admin Setting Edit
從Admin Setting頁面，點Edit按鈕

![](https://i.imgur.com/xB008MK.png)

:::spoiler Username 管理者名稱
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_NAME  | VARCHAR(100) |

#### 檢查規則

:::
:::spoiler Email 管理者電子信箱
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_MAIL  | VARCHAR(50) |

#### 檢查規則

:::
:::spoiler Account 管理者ID編號
| Table    | Column   | Datatype |
| -------- | -------- | -------- |
| SYS_USER   | USER_ID  | VARCHAR(30) |

#### 檢查規則
無法變更管理者ID編號
:::

### New Account
從Admin Setting頁面，點Add按鈕

![](https://i.imgur.com/w58MdwJ.png)
