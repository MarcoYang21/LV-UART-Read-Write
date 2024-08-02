# LV-UART-Read-Write
目前這個專案一共有五種寫法來做UART讀寫動作
1. 基本資料流
2. JKI state machine
3. actor framework
4. Worker
5. DQMH

## The flow chart
```mermaid
flowchart TD
    A[開啟 COM 埠] --> B[設定讀取時不檢查結束字元]
    B --> C{是否有資料要寫入？}
    C -->|沒有| G{Buffer 是否有資料可以讀取？}
    C -->|有資料要寫入| F[進行資料寫入]
    F --> G
    G -->|沒有| I[等待 200 毫秒]
    G -->|有資料| H[讀取資料]
    I --> G
    H --> K{字串長度是否滿足條件？}
    K -->|是| D{是否停止寫入作業？}
    K -->|否| G
    D -->|否| C
    D -->|是| E[關閉 COM 埠]
    E --> J[結束]

