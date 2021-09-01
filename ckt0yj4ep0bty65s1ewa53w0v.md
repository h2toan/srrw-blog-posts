## Những hàm hữu ích ở Google Sheet mà tôi tự viết

Google Sheet cung cấp thư viện hàm có sẵn khá tiện ích cho người sử dụng. Tuy nhiên, để đáp ứng tốt được công việc thì cần kết hợp các hàm lại với nhau để xử lí.  

Bài viết này tôi sẽ tổng hợp một số hàm tự viết mà có thể sẽ giúp các bạn hoàn thành được công việc của mình một cách hiệu quả hơn.

Bắt đầu nhé!

## 1. Hàm viết hoa chữ cái đầu mỗi từ, áp dụng cho Tiếng Việt

Ngoài các hàm UPPER và LOWER, Google Sheet cung cấp 1 hàm PROPER dùng để viết hoa chữ cái đầu mỗi từ, rất hữu ích khi sử dụng để viết hoa tên người:

```
PROPER('forrest gump') // output: Forrest Gump
```

Dở thay hàm này lại không hoạt động đúng với các kí tự tiếng Việt. Tôi nghĩ nhiều khả năng do hàm sử dụng regex để tìm chữ cái cần viết hoa, mà các cú pháp word boundary của regex vốn chẳng ưa gì Tiếng Việt rồi. Ví dụ:

```
PROPER('đỗ phương thảo') // output: Đỗ Phương ThảO
```

Tới công chuyện rồi đây ^^. Để khắc phục nhược điểm này, tôi dùng hàm SPLIT để tách đoạn text thành từng từ và dùng regex để viết hoa chữ cái đầu, sau đó lại nối lại bằng JOIN

```
JOIN(" ",ARRAYFORMULA(REGEXREPLACE(SPLIT(A1," "),"^.",UPPER(REGEXEXTRACT(SPLIT(A1," "),"^.")))))

/* input: đỗ phương thảo => output: Đỗ Phương Thảo */
```

Các bạn chỉ việc thay A1 bằng ô text cần chuyển đổi để sử dụng nhé. 

_____
to be updated
