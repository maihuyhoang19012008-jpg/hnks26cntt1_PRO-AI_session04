

### **PHẦN 1: PHÂN TÍCH & LỰA CHỌN PHƯƠNG PHÁP**

-   **Bối cảnh và Vấn đề:** Tự động hóa việc xử lý đơn hàng từ tin nhắn khách hàng. Rủi ro lớn nhất là khách nhắn thiếu thông tin 
-   **Phương pháp chọn:**
    
    1.  **Chain-of-Thought (CoT):** Bắt AI lập luận từng bước kiểm tra điều kiện (`IF...THEN...`) để không bỏ sót lỗi.
        
    2.  **Prompt Chaining:** Chia làm 2 bước rõ rệt (Bước 1: Lọc dữ liệu & bắt lỗi -> Bước 2: Viết tin nhắn phản hồi) để AI không bị quá tải.
        

### **PHẦN 2: THIẾT KẾ GIẢI PHÁP (I/O)**

-   **Input:** Danh mục sản phẩm của cửa hàng + Tin nhắn thô của khách.
    
-   **Output:** Bảng kiểm tra trạng thái đơn hàng (Hợp lệ / Lỗi) + Tin nhắn phản hồi tự động cho khách.
    

### **PHẦN 3: NỘI DUNG PROMPT & KẾT QUẢ CHẠY THỬ**

#### **Prompt 1: Kiểm tra lỗi & Tính tiền (Áp dụng CoT)**

> **[Prompt]:** Bạn là trợ lý xử lý đơn hàng. Dựa vào **[Danh mục]**: Áo thun (200k), Quần Jean (350k). Freeship đơn từ 500k, dưới 500k ship 30k. Hãy xử lý danh sách khách hàng dưới đây theo các bước sau:
> 
> -   **Bước 1:** Kiểm tra sản phẩm có trong danh mục không?
>     
> -   **Bước 2:** Kiểm tra thông tin (Tên, SĐT đủ 10 số, Địa chỉ) có đầy đủ không? Nếu thiếu -> Ghi rõ lỗi, **tuyệt đối không bịa thêm**.
>     
> -   **Bước 3:** Nếu hợp lệ thì tính tổng tiền.
>     
> -   **Đầu ra:** Xuất thành bảng gồm: `Khách | Phân tích CoT | Trạng thái | Tổng tiền`.
>     
> 
> **[Dữ liệu]:**
> 
> 1.  Chị Lan, 0912345678, số 10 Cầu Giấy, lấy 2 áo thun.
>     
> 2.  Anh Hùng, lấy 1 quần jean, giao về Q.1 HCM (Thiếu SĐT).
>     

-   **Kết quả AI trả ra:**
    
    -   **Chị Lan:** Đủ thông tin, mua 2 áo (400k) + ship 30k = **430.000đ** | **Trạng thái:**  `HỢP LỆ`
        
    -   **Anh Hùng:** Thiếu SĐT, không đủ điều kiện lên đơn | **Trạng thái:**  `LỖI (Thiếu SĐT)`
        

#### **Prompt 2: Tạo tin nhắn phản hồi (Prompt Chaining)**

> **[Prompt]:** Dựa vào kết quả bảng trên, hãy đóng vai nhân viên CSKH viết tin nhắn gửi khách:
> 
> -   Đơn hợp lệ: Cảm ơn và báo tổng tiền.
>     
> -   Đơn lỗi: Nhắc khéo khách bổ sung thông tin thiếu.
>     

-   **Kết quả AI trả ra:**
    
    1.  _Gửi Chị Lan:_ "Dạ Shop xác nhận đơn 2 Áo thun, tổng tiền kèm ship là 430.000đ. Shop gửi về số 10 Cầu Giấy ạ!"
        
    2.  _Gửi Anh Hùng:_ "Chào anh Hùng, anh đặt Quần Jean nhưng đang quên để lại SĐT. Anh bổ sung giúp Shop để em lên đơn nhé!"
