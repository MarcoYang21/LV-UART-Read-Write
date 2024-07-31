# LV-UART-Read-Write
## simple UART Read-Write LabVIEW code

## The flow chart
flowchart TD
    A[開啟 COM 埠] --> B{是否有資料要寫入？}
    B -->|沒有| F{Buffer 是否有資料可以讀取？}
    B -->|有資料要寫入| E[進行資料寫入]
    E --> F
    F -->|沒有| H[等待 200 毫秒]
    F -->|有資料| G[讀取資料]
    H --> F
    G --> C{是否停止寫入作業？}
    C -->|否| B
    C -->|是| D[關閉 COM 埠]
    D --> I[結束]
