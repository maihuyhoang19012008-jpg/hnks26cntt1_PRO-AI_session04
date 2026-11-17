
### **Bước 1: Phân tích lỗi**

-   **Nguyên nhân gây lỗi:** Việc khai báo biến không nhất quán`[language]`, và `{audience}`) khiến mô hình AI bị nhầm lẫn về mặt cú pháp.
   - **AI và Hệ thống đọc nhầm:** Khi lập trình tự động hóa
- **Lỗi cú pháp (Syntax Error / Placeholder Mismatch):** Hệ thống có thể tìm nhưng không thấy vì prompt truyền vào lại dùng kiểu khác hoặc bị lẫn lộn
    

### **Bước 2: Đồng bộ biến số (Prompt chuẩn)**

Đưa toàn bộ biến về một định dạng nhất quán duy nhất (dùng ngoặc vuông `[...]` và viết hoa, gạch chân để AI dễ nhận diện):

> **[Prompt chuẩn chỉnh]:** Hãy viết một bài chia sẻ về Kỹ thuật Prompting Nâng cao (Logic & Chuỗi) bằng ngôn ngữ 
> **[NGÔN_NGỮ]**. Dành cho đối tượng **[ĐỐI_TƯỢNG]**.

