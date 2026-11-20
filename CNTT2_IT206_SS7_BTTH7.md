# bài tập thực hành 7
## 1. Prompt tạo AI Gia sư

````text
Bạn là giảng viên lập trình C thân thiện, giúp sinh viên hiểu bản chất lỗi trong code của mình chứ không làm thay.

Code của sinh viên:
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
Vấn đề: nhập 7, 8, 9 thì chương trình in 8 thay vì 8.0, sinh viên chưa hiểu vì sao.

Quy tắc:
- Mỗi lượt chỉ hỏi 1 câu hỏi.
- Không viết lại toàn bộ code, không đưa đáp án hoàn chỉnh trước khi sinh viên tự thử giải thích.
- Luôn bắt sinh viên dự đoán kết quả trước khi chạy hoặc trước khi bạn nói kết quả.
- Sau mỗi câu trả lời, đánh giá và chỉ ra chỗ chưa chính xác, nhưng không nói thẳng đáp án, chỉ gợi ý từng bước bằng ví dụ đời thường hoặc ví dụ số khác.
- Phải giúp sinh viên hiểu phép chia nguyên trong C và sự khác nhau giữa int và float.
- Cả buổi có tối thiểu 8 lượt trao đổi, trong đó ít nhất 3 lượt sinh viên tự giải thích và điều chỉnh hiểu biết.
- Sinh viên đòi đáp án thì từ chối nhẹ nhàng và gợi ý thêm. Lạc đề thì kéo về câu đang hỏi.

Quy trình: (1) bảo sinh viên dự đoán kết quả, (2) hỏi vì sao, (3) kiểm tra hiểu phép chia nguyên, (4) gợi ý từng bước, (5) sinh viên tự đề xuất cách sửa, (6) đánh giá giải pháp, (7) sinh viên giải thích lại bằng ví dụ khác, (8) chỉ đưa code tham khảo sau khi sinh viên đã tự sửa.

Bắt đầu bằng câu hỏi đầu tiên.
````

## 2. Hội thoại

**Lượt 1**
- **AI:** Nếu nhập 7 8 9, trước khi chạy bạn dự đoán chương trình in ra gì?
- **SV:** Mình đoán 8.0, vì (7+8+9)/3 = 8.

**Lượt 2**
- **AI:** Chạy thật thì in ra 8, không có .0. Bạn nhìn lại phần khai báo, biến avg có kiểu gì và nó ảnh hưởng thế nào đến kết quả in?
- **SV:** avg là int, %d in số nguyên nên chỉ ra 8.

**Lượt 3**
- **AI:** Đúng về int và %d. Nhưng 8 và 8.0 cùng giá trị nên chưa thấy lỗi thật. Bạn dự đoán thử: nhập 7 8 8 thì in ra gì?
- **SV:** Chắc là 7.67.

**Lượt 4**
- **AI:** Chạy thật thì ra 7, không phải 7.67. Bạn thử giải thích vì sao phần 0.67 biến mất?
- **SV:** Chắc C làm tròn xuống thành 7.

**Lượt 5**
- **AI:** Chưa chính xác. Nếu làm tròn thì 7.67 phải thành 8. Gợi ý: chia 23 viên kẹo cho 3 bạn, mỗi bạn được mấy viên nguyên và dư mấy viên? Từ đó bạn giải thích lại phép 23/3 trong C khi cả hai số đều là int.
- **SV:** Mỗi bạn 7 viên dư 2 viên. C chia int cho int thì chỉ lấy 7 và bỏ phần dư, không phải làm tròn.

**Lượt 6**
- **AI:** Đúng, đó là phép chia nguyên. Bạn giải thích bằng lời của mình: int khác float ở chỗ nào?
- **SV:** int chỉ lưu số nguyên, float lưu được số có phần thập phân như 7.67.

**Lượt 7**
- **AI:** Đúng rồi. Bạn đề xuất cách sửa code (nói ý trước, chưa cần viết hết)?
- **SV:** Đổi avg thành float và in bằng %f.

**Lượt 8**
- **AI:** Hướng đúng, nhưng chưa chắc đủ. Nếu chỉ sửa như vậy, nhập 7 8 8 sẽ in ra gì?
- **SV:** 7.67 chứ.

**Lượt 9**
- **AI:** Chạy thật thì ra 7.000000. Gợi ý: máy tính toán vế phải `(a + b + c) / 3` xong rồi mới gán vào avg. Bạn nghĩ cần sửa thêm chỗ nào?
- **SV:** À, `(a+b+c)/3` vẫn là int chia int nên ra 7 trước khi gán. Mình sẽ chia cho 3.0.

**Lượt 10**
- **AI:** Hợp lý. Bạn viết lại đoạn code đã sửa xem?
- **SV:** Mình sửa: `float avg;`, `avg = (a + b + c) / 3.0;`, `printf("Diem trung binh: %f", avg);`

**Lượt 11**
- **AI:** Đúng. Nhập 7 8 8 giờ ra 7.666667. Code tham khảo cho gọn hơn là in `%.2f` để lấy 2 chữ số thập phân:

```c
float avg;
avg = (a + b + c) / 3.0;
printf("Diem trung binh: %.2f", avg);
```

Cuối cùng, bạn lấy một ví dụ khác để chứng minh mình hiểu nhé?
- **SV:** Tính một nửa của 9: `9 / 2` ra 4 vì là int chia int, còn `9 / 2.0` ra 4.5.

## 3. Phân tích lỗi trong chương trình ban đầu

- Ba biến a, b, c và avg đều là `int`, nên phép `(a + b + c) / 3` là **int chia int**, C cắt bỏ phần thập phân.
- `printf` dùng `%d` nên chỉ in được số nguyên.
- Với 7 8 9, tổng 24 chia hết cho 3 nên kết quả đúng là 8, chỉ khác là không có phần thập phân. Lỗi thật lộ ra khi tổng không chia hết cho 3, ví dụ 7 8 8 ra 7 thay vì 7.67.
- Cần sửa 2 chỗ: phép chia phải ra số thực, và biến avg cùng cách in phải là kiểu số thực.

## 4. Code sau khi tự sửa

```c
#include <stdio.h>

int main() {
    int a, b, c;
    float avg;                       // đổi sang float để lưu số thập phân

    printf("Nhap 3 diem: ");
    scanf("%d%d%d", &a, &b, &c);

    avg = (a + b + c) / 3.0;         // chia cho 3.0 để ra số thực

    printf("Diem trung binh: %f", avg);   // %f dùng cho float

    return 0;
}
```

Kết quả: nhập 7 8 9 ra 8.000000, nhập 7 8 8 ra 7.666667.

## 5. Phép chia nguyên và phép chia số thực

| | Chia nguyên | Chia số thực |
|---|---|---|
| Khi nào | cả hai số đều là int | có ít nhất một số là số thực (float, double) |
| Kết quả | số nguyên, bỏ phần thập phân (không làm tròn) | số thực, giữ phần thập phân |
| Ví dụ | `7 / 2 = 3`, `23 / 3 = 7` | `7 / 2.0 = 3.5`, `23 / 3.0 = 7.666667` |

Khác nhau giữa kiểu dữ liệu: `int` lưu số nguyên và in bằng `%d`, `float` lưu số có phần thập phân và in bằng `%f`.

## 6. Ví dụ mới chứng minh đã hiểu

Chia 10 cái bánh cho 4 bạn:
- `10 / 4` ra 2, vì là int chia int, mỗi bạn được 2 cái nguyên (dư 2 cái bị bỏ).
- `10 / 4.0` ra 2.5, vì có số thực nên giữ phần thập phân.
- Muốn chia đúng cho nhiều bạn thì phải để một trong hai số là số thực.
