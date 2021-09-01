## Những hàm hữu ích ở Google Sheet mà tôi tự viết

## Hàm viết hoa chữ cái đầu mỗi từ, áp dụng cho tiếng việt

Để chuyển đổi chữ hoa chữ thường trong Google Sheet, ta có thể dùng các hàm UPPER và LOWER:

```
UPPER('forrest gump') // output: FORREST GUMP

LOWER('FORREST GUMP') // output: forrest gump
```


Ngoài các hàm UPPER và LOWER, Google Sheet cung cấp 1 hàm PROPER dùng để viết hoa chữ cái đầu mỗi từ, rất hữu ích khi sử dụng để viết hoa tên người:

```
PROPER('forrest gump') // output: Forrest Gump
```

Dở thay hàm này lại không hoạt động đúng với các kí tự tiếng Việt. Tôi nghĩ nhiều khả năng do hàm sử dụng regex để tìm chữ cái cần viết hoa, mà các cú pháp word boundary của regex vốn chẳng ưa gì Tiếng Việt rồi. Ví dụ:

```
PROPER('đỗ phương thảo') // output: Đỗ Phương ThảO
```

Tới công chuyện rồi đây. Để khắc phục nhược điểm này, tôi có viết 1 hàm, áp dụng chuẩn xác 100% đối với ngôn ngữ mẹ đẻ tôi:

```
JOIN(" ",ARRAYFORMULA(REGEXREPLACE(SPLIT(A1," "),"^.",UPPER(REGEXEXTRACT(SPLIT(A1," "),"^.")))))

/* input: đỗ phương thảo => output: Đỗ Phương Thảo */
```

Các bạn chỉ việc thay A1 bằng ô text cần chuyển đổi để sử dụng nhé. 
