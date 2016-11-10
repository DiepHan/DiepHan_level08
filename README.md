# CẤP PHÁT BỘ NHỚ ĐỘNG  
Ngôn ngữ C cung cấp cho chúng ta 4 hàm: `malloc`, `calloc` , `realloc` để cấp phát và `free` để thu hồi.   
Trong C, bốn hàm `malloc`, `calloc`, `realloc` và `free` nằm trong thư viện `stdlib.h` hoặc` alloc.h`, trước khi sử dụng các bạn phải khai báo thư viện này.  
### HÀM MALLOC  
>Cú pháp: `void* malloc(size_t size);`  
>Ý nghĩa: Cấp phát vùng nhớ động có kích thức size byte.  

- Để đảm bảo cấp phát đủ bộ nhớ cho một mảng, ta thường sử dụng `malloc(n*sizeof(data_type))` với n là số phần tử. Toán tử `sizeof(kiểu_dữ_liệu)` trả về kích thước của kiểu dữ liệu (do kích cỡ một kiểu dữ liệu không cố định ở những kiến trúc máy tính khác nhau).  
Với một mảng có kiểu dữ liệu xác định nên ta phải ép kiểu để phù hợp với kiểu dữ liệu của mảng.  
Hàm malloc chỉ cấp phát mà không khởi tạo giá trị ban đầu cho các biến.  


**VD:**
```c
//cấp phát mảng động kiểu int với 5 phần tử
int *p = (int*)malloc(5*sizeof(int));
 
//cấp phát chuỗi động có 11 phần tử
char *str = (char*)malloc(11*sizeof(char));
```  
### HÀM CALLOC  
>Cú pháp: `void* calloc(size_t num, size_t size);`  
>Ý nghĩa: Cấp phát mảng động có num phần tử có kích thước size byte.  


-Tương tự hàm malloc, ta cũng cần ép kiểu cho phù hợp với kiểu dữ liệu mảng. Sau khi cấp phát, các phần tử sẽ được gán giá trị 0.  
**VD:**  
```c
int *p = (int*)calloc(5, sizeof(int));
char *str = (char*)calloc(11, sizeof(char));
```  
### HÀM REALLOC  
>Cú pháp: `void* realloc(void *ptr, size_t size);`  
>Ý nghĩa: Thay đổi kích thước vùng nhớ được trỏ bởi con trỏ ptr với kích thước mới là size byte.  


**VD:**  
```c
int *p = (int*)malloc(5*sizeof(int));
int *q = (int*)realloc(p, 10*sizeof(int));
```  
### HÀM FREE  
>Cú pháp: `void free(void *p);`  
>Ý nghĩa: Giải phóng vùng nhớ trỏ bởi con trỏ p.  
 
 
- Phải luôn nhớ giải phóng bộ nhớ động khi không dùng đến nữa.  
**VD:**  
```c
int *a = (int*)malloc(512);
free(a);  
```





