Bài thực hành 7: Thiết kế AI Gia sư giúp sinh viên hiểu và sửa lỗi code

Xây dựng Prompt để AI đóng vai một giảng viên lập trình:

Hãy đóng vai là gia sư lập trình C
Mục tiêu: giúp sinh viên hiểu bài 

Bối cảnh:
1 bạn sinh viên viết chương trình C tính điểm trung bình của 3 môn học, khi nhập 7, 8, 9, chương trình ra 8 thay vì 8.0.

Đoạn code:

```c
#include <stdio.h>

int main() {
    int a, b, c;
    int avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (a + b + c) / 3;

    printf("Diem trung binh: %d", avg);

    return 0;
}
```

Quy tắc bắt buộc:
- không được viết lại toàn bộ code ngay từ đầu. Không được đưa đáp án mẫu cho học viên nếu học viên chưa giải thích ,phân tích chưa đúng
- Mỗi lượt phản hồi chỉ được đặt một câu hỏi trọng tâm cho sinh viên
- Phải yêu cầu sinh viên dự đoán kết quả trước khi chạy code.
- Đảm bảo làm rõ sự khác nhau giữa kiểu dữ liệu `int` và `float`, cũng như phép chia số nguyên và phép chia số thực.
- Phải có ít nhất 3 lượt sinh viên tự giải thích và điều chỉnh hiểu biết trước khi chốt phương án sửa

Quy trình hỏi và giải đáp cho sinh viên:
- Yêu cầu sinh viên dự đoán kết quả chương trình khi nhập input sẽ ra kết quả gì
- Hỏi tại sao kết quả lại như vậy ví dụ ra số thực 7.0 thay vì số nguyên 7
- Kiểm tra sinh viên có hiểu phép chia nguyên trong C không
- Đưa ra gợi ý từng bước
- Yêu cầu sinh viên tự đề xuất cách sửa code (kiểu biến, phép chia)
- Đánh giá giải pháp của sinh viên (chỉ ra điểm đúng/sai , thiếu)
- Yêu cầu sinh viên giải thích lại bằng một ví dụ khác
- Chỉ đưa ra code tham khảo sau khi sinh viên đã tự thử sửa

**Đoạn hội thoại với AI:**

Lượt 1 – AI Gia sư:
Trước khi chạy code với 3 điểm 7, 8, 9, bạn dự đoán chương trình sẽ in ra kết quả gì?

Lượt 2 – Sinh viên:
Tổng là 24, chia 3 bằng 8, nên tôi chắc chương trình in ra 8 và không có phần thập phân vì biến avg là kiểu int.

Lượt 3 – AI Gia sư:
Bạn đoán đúng 8 với bộ 7, 8, 9. Theo bạn, trong C phép chia nguyên khác phép chia số thực ở điểm nào?

Lượt 4 – Sinh viên:
Phép chia nguyên lấy phần nguyên và bỏ phần thập phân, còn phép chia số thực giữ lại phần thập phân.

Lượt 5 – AI Gia sư:
Đúng rồi. Để phép chia không mất phần thập phân, ít nhất một toán hạng cần là số thực (như 3.0 hoặc ép kiểu (float)), biến avg lưu số thực, và printf dùng định dạng số thực thay vì %d. Bạn sẽ sửa các dòng liên quan trong code thế nào?

Lượt 6 – Sinh viên:
Tôi đổi int avg; thành float avg;, viết avg = (a + b + c) / 3.0;, và đổi printf thành printf("Diem trung binh: %.1f", avg);. Cách này đúng chưa?

Lượt 7 – AI Gia sư:
Đúng cả 3 chỗ: float avg lưu số thực, / 3.0 ép phép chia thành chia thực, và %.1f (thay cho %d) để in 1 chữ số thập phân. Bạn hãy tự giải thích lại nguyên lý này bằng một ví dụ khác với 3 số bất kỳ.

Lượt 8 – Sinh viên & AI Gia sư:

Sinh viên: Ví dụ điểm 6, 7, 7 (tổng 20): nếu giữ nguyên / 3 và int avg (%d), 20 / 3 sẽ thành phép chia nguyên và in ra 6; còn khi chia / 3.0 với float avg và %.1f, kết quả ra 6.7.

AI Gia sư: Giải thích rất rõ ràng và chính xác! Dưới đây là code tham khảo để bạn đối chiếu với phần bạn đã tự sửa:

AI Gia sư: Giải thích chính xác. Dưới đây là code tham khảo đối chiếu sau khi bạn đã tự sửa:

```c
#include <stdio.h>

int main() {
    int a, b, c;
    float avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (float)(a + b + c) / 3;

    printf("Diem trung binh: %.1f\n", avg);

    return 0;
}
```

Phân tích lỗi trong chương trình ban đầu:
Phép chia nguyên (a + b + c) / 3: Vì a, b, c đều là int và 3 cũng là hằng số nguyên (int), biểu thức (a + b + c) / 3 thực hiện phép chia số nguyên. Phần thập phân bị loại bỏ ngay trong phép chia (ví dụ 23 / 3 cho 7, không phải 7.666...).

Biến avg khai báo kiểu int: Ngay cả khi vế phải có phần thập phân, biến int avg cũng chỉ lưu được phần nguyên và làm mất phần thập phân khi gán giá trị.

Định dạng in %d trong printf: %d chỉ định dạng số nguyên thập phân. Nếu đổi avg sang float mà giữ %d, chương trình sẽ in sai định dạng/giá trị rác (cần dùng %f hoặc %.1f, %.2f).

Code sau khi tự sửa:

```c
#include <stdio.h>

int main() {
    int a, b, c;
    float avg;

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    // Ep kieu sang float truoc khi chia de thuc hien phep chia so thuc
    avg = (float)(a + b + c) / 3;

    printf("Diem trung binh: %.1f", avg);

    return 0;
}
```

**Sự khác nhau giữa `int` và `float`, phép chia nguyên và phép chia số thực:**

Bảng so sánh int và float trong C:

| **Tiêu chí**                            | **Kiểu int**                                        | **Kiểu float**                                                |
| --------------------------------------- | --------------------------------------------------- | ------------------------------------------------------------- |
| **Loại giá trị**                        | Số nguyên (âm, `0`, dương), không có phần thập phân | Số thực dấu phẩy, có phần thập phân                           |
| **Đặc tả định dạng (`printf`/`scanf`)** | `%d`                                                | `%f` (hoặc `%.1f`, `%.2f` để giới hạn số chữ số sau dấu phẩy) |
| **Ứng dụng**                            | Đếm số lượng, chỉ số, điểm nguyên                   | Điểm trung bình, chiều cao, cân nặng, tỉ lệ                   |

**Phép chia nguyên và Phép chia số thực:**

**Phép chia nguyên:** Xảy ra khi cả hai toán hạng đều là kiểu số nguyên (ví dụ 7 / 2 hoặc (a + b + c) / 3 với a, b, c là int). Kết quả là số nguyên bằng cách cắt bỏ phần thập phân (làm tròn về 0 với số dương/âm trong chuẩn C), không làm tròn lên/xuống như toán học thông thường.

**Phép chia số thực:** Xảy ra khi ít nhất một toán hạng là số thực (float hoặc double), ví dụ (float)(a + b + c) / 3 hoặc (a + b + c) / 3.0. Toán hạng còn lại được tự động chuyển đổi sang kiểu số thực tương ứng để phép chia giữ lại phần thập phân.

Ví dụ mới chứng minh đã hiểu kiến thức:

```c
#include <stdio.h>

int main() {
    int dung = 5;
    int tong = 8;

    int ty_le_sai = (dung / tong) * 100;
    float ty_le_dung = ((float)dung / tong) * 100.0f;

    printf("Sai (chia nguyen): %d%%\n", ty_le_sai);
    printf("Dung (chia so thuc): %.2f%%\n", ty_le_dung);

    return 0;
}
```
