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
# HEAP MEMORY   


### CẤP PHÁT  


- Heap là một vùng nhớ rất rộng có sẵn để chương trình sử dụng. Chương trình có thể yêu cầu vùng hoặc khối nhớ để nó sử dụng ở trong heap. Để cấp phát một khối nhớ, chương trình làm yêu cầu minh bạch gọi hàm cấp phát của heap. Hàm cấp phát sẽ để riêng một khối nhớ vừa được yêu cầu kích cở trong heap và trả về con trỏ trỏ vào nó. Giả sủ chương trình làm ba cấp phát yêu cầu cấp phát động , tổ chức nó riêng biệt để lưu trữ ảnh GIF trong heap , mỗi kích cỡ là 1024 bytes. Sau khi yêu cầu cấp phát, bộ nhớ được nhìn như thế này :  
![](http://3.bp.blogspot.com/-Az6dYqNmWD4/Vnkexr35piI/AAAAAAAABE0/9njFUzxIOeM/s1600/allocation%2Bin%2Bheap.PNG)  
- Mỗi cấp phát yêu cầu dành riêng một vùng nhớ liên tục với kích cỡ được yêu cầu trong heap và trả về con trỏ trỏ đến khỗi nhớ đó cho chương trình. Bởi vì khỗi này luôn được trỏ bởi con trỏ.  
- Trong ví dụ trên, ba khối được cấp phát LIÊN TỤC TỪ PHÍA DƯỚI của bộ nhớ heap và mỗi khối là 1024 byte như kích cỡ được yêu cầu. Trên thực tế quản lý heap "heap manager" có thể cấp phát khối nhớ bất cứ nơi nào nó muốn trong heap miễn là những khối không chồng chéo lên nhau và có ít nhất một yêu cầu có kích cỡ. Tại một vài thời điểm cụ thể, một vài vùng trong heap đã được cấp phát cho chương trình , vì vậy nó được coi là đang sử dụng "in use". Vài vùng khác chưa được ủy thác nên nó được coi là tự do "free" và có sãn để đáp ứng cho yêu cầu cấp phát. Quản lý vùng nhớ heap tự có riêng của mình câu trúc dữ liệu private "private data structures " để ghi lại đâu là vùng nhớ của heap đã được giao phó cho mục đích tại một vài thời điểm. Quản lý heap đáp ứng cho mỗi yêu cầu cấp phát thừ khối bộ nhớ đang tự do "free memory" sau đó cập nhật nó vào private dât structures để ghi nó lại là bộ nhớ đó đang trong sử dụng.

### THU HỒI  
- Khi chương trình đang sử dụng khối nhớ kết thúc, nó làm một yêu cầu thu hồi (deallocation) minh bạch để chỉ cho heap manager rằng chương trình đó đã kết thúc bây giờ với khối nhớ. Heap manager cập nhất private data structures của nó chỉ ra rằng vùng nhớ đã chiếm đóng đã free trở lại và vì vậy có thể tái sử dụng "re-used" để đáp ứng cho tính năng yêu cầu allocation. Đâu là những gì mà heap muốn thấy nếu chương trình deallocates khối thử hai của ba khối :  
![](http://2.bp.blogspot.com/-p3WkPK-oALI/Vnke-GdeUPI/AAAAAAAABFA/zpXM6-RzqfM/s1600/deallocation%2Bin%2Bheap.PNG)  
- Sau khi deallocation, con trỏ tiếp tục trỏ vào khối đã bị deallocated ngay lúc đó. Nhưng chương trình không được truy cập vào vùng nhớ đã bị deallocated. Đó là lý do tại sao con trỏ được vẽ màu xám - CON TRỎ VẪN Ở ĐÓ NHƯNG NÓ KHÔNG ĐƯỢC SỬ DỤNG. Thỉnh thoảng code sẽ đặt con trỏ trỏ tới NULL ngay tức thì sau khi deallocation được làm một cách minh bạch thực tế điều này khồn có giá trị.  


### VD:  
### Cấp phát một khối kiểu int trong heap, lưu số 42 vào trong khối đó, và sau đó deallocate nó 
![](http://2.bp.blogspot.com/-R3KGqaNkIos/VnkfD5YLIHI/AAAAAAAABFQ/e_8-FEGxFOA/s1600/local%2Band%2Bheap%2BT1.PNG)   

----
![](http://2.bp.blogspot.com/-U7Ki58ncns8/VnkfDwyfLvI/AAAAAAAABFU/u5uMq5qyThQ/s1600/local%2Band%2Bheap%2BT2.PNG)  

----
![](http://1.bp.blogspot.com/-7-j400MYV1w/VnkfD3uquCI/AAAAAAAABFg/MMmV-snO2WQ/s1600/local%2Band%2Bheap%2BT3.PNG) 










