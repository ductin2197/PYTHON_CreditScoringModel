# 📊 Credit Scoring Engine & Risk Analytics Framework

## 📈 Key Risk Analytics & Insights
Đây là kết quả phân tích danh mục 1.000 khách hàng giả lập được trích xuất trực tiếp từ mô hình:

![Credit Scoring Dashboard](PREVIEW.png)

* **Tỷ lệ phê duyệt tối ưu:** Hệ thống tự động kiểm soát tỷ lệ duyệt ở mức **88.9%**, đảm bảo khả năng mở rộng tệp người dùng sành sỏi công nghệ mà không nới lỏng tiêu chuẩn an toàn.
* **Tương quan rủi ro rõ rệt:** Biểu đồ phân phối chứng minh hiệu quả hệ thống khi cô lập hoàn toàn nhóm khách hàng trễ hạn từ 3 lần trở lên vào phân khúc **REJECT** (Dải điểm dưới 500).

## 🧑‍💻 WORKING STEPS
```mermaid
flowchart LR
    A[Gathering Data] --> B[Processing]
    B --> C[Calculating Credit Score]

    C -->|Score < 500| D[Reject]
    C -->|Score ≥ 500| E[Approved]

    E -->|500 ≤ Score < 600| F[Credit Limit: 5M VND]
    E -->|Score ≥ 600| G[Credit Limit: 10M VND]

    %% Styling (no white / black, no duplicate colors)
    style A fill:#E3F2FD,stroke:#1565C0,stroke-width:2px,color:#0D47A1
    style B fill:#FFF3E0,stroke:#EF6C00,stroke-width:2px,color:#E65100
    style C fill:#E1F5FE,stroke:#0277BD,stroke-width:2px,color:#01579B
    style D fill:#FCE4EC,stroke:#C62828,stroke-width:2px,color:#B71C1C
    style E fill:#E8F5E9,stroke:#2E7D32,stroke-width:2px,color:#1B5E20
    style F fill:#F3E5F5,stroke:#6A1B9A,stroke-width:2px,color:#4A148C
    style G fill:#E0F2F1,stroke:#00695C,stroke-width:2px,color:#004D40
```
---
## 🧮 Risk Factor Scoring Framework (Bảng tra cứu điểm số)
Hệ thống vận hành dựa trên cơ chế chấm điểm động (Dynamic Scorecard) với thang điểm chuẩn từ **300 đến 850**
(Thang điểm này là thang comparable với benchmark của FICO và là thang được sử dụng rộng rãi trên thị trường):

| Tiêu chí phân tích | Khoảng giá trị (Bin) | Điểm cộng / trừ |
| :--- | :--- | :---: |
| **Thâm niên dùng Ví** | >= 24 tháng <br> 6 - 24 tháng <br> < 6 tháng | **+50** <br> **+20** <br> **-25** |
| **Lịch sử chậm thanh toán** | 0 lần <br> 1 lần <br> 2 lần <br> >= 3 lần | **+60** <br> **-20** <br> **-60** <br> **-120** |
| **Thói quen thanh toán Hóa đơn** | >=10 lần <br> >=6 lần <br> >=3 lần <br> Chưa đủ thông tin | **+30** <br> **+15** <br> **+5** <br> **+0** |
| **Tổng tiền giao dịch qua ví mỗi tháng** | >=10tr <br> >=3 <br> >=1tr <br> <1tr | **+35** <br> **+20** <br> **+0** <br> **-15** |

## 🐍 Python Highlight 

```python
def make_credit_decision(score):
    if score >= 600:
        return 'APPROVE', '10,000,000 VND'
    elif score >= 500:
        return 'APPROVE', '5,000,000 VND'
    else:
        return 'REJECT', '0 VND'

# Áp dụng quyết định
df_customers[['Decision', 'Max_Limit']] = df_customers['Credit_Score'].apply(lambda s: pd.Series(make_credit_decision(s)))
df_customers.head()
```

## 💻 Tech Stack & Core Logic
* **Language:** Python (thực hiện bằng Google Colab)
* **Libraries:** `pandas` (Data simulation & manipulation), `matplotlib` & `seaborn` (Statistical visualization).
* **Decision Logic:**
  * Điểm >= 600: **APPROVE** | Hạn mức 10,000,000 VND
  * Điểm 500 - 599: **APPROVE** | Hạn mức 5,000,000 VND
  * Điểm < 500: **REJECT** | Hạn mức 0 VND
