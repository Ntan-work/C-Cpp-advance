# C-Cpp-advance

BÀI 1: COMPILER-MACRO
Khi run file chương trình file.c hoặc file.h thì compiler nó sẽ tạo ra file .exe, quá trình tạo ra file .exe này sẽ trải qua 4 bước
Bước 1: tiền xử lý Preprocessor
-	Đây là bước biến đổi các file .c và file.h thành các file.i
-	Dùng câu lệnh 
gcc -E main.c -o main.i
-	Các file .i này chứa các thông tin code trong file.c 
-	Giả sử như trong file .c có include các thư viện <stdio.h> hay bất kì 1 thư viện nào thì trong file .i sẽ truy cập các file thư viện đó và copy toàn bộ vào file.i.
-	Các thư viện được include vào sẽ phân biệt ra là thư viện hệ thống hoặc thư viện do người dùng tạo ra đã được add vào trong project (<stdio.h> hoặc là “stdio.h”),
-	Trong file.i, sau khi đã copy các thư viện đã include thì nó sẽ copy các hàm và các câu lệnh ở trong main.c đã làm
-	Có điều nó sẽ thay thế các giá trị mà các biến được khai báo bằng macro #define 
-	Đối với các lệnh comment trong file main.c thì trong file .i sẽ bị loại bỏ
-	Trong tiền xử lý thướng hay sử dụng các macro. Dùng để chỉ những thông tin được xử lý ở quá trình tiền xử lý. Chia làm 3 nhóm chính:
o	#include
o	#define, #undef
o	#if, #elif, #else, #ifdef, #ifndef
-	Ứng dụng của macro: 
o	Dùng để thay thế một chuỗi mã nguồn bằng một chuỗi khác trước khi chương trình biên dịch.
o	Giúp giảm lặp lại mã, dễ bảo trì chương trình.
a)	Chỉ thị tiền xử lý #include
Chỉ thị #include dùng để chèn nội dung của một file vào mã nguồn chương trình.
ứng dụng: 
-	tái sử dụng mã nguồn
-	phân chia chương trình thành các phần nhỏ, giúp quản lý mã nguồn hiệu quả
Chỉ thị #include hay còn gọi là chỉ thị bao hàm tệp được phân chia thành 2 loại
-	<> :    khi nhấn runcode thì compiler sẽ biết vị trí mà tìm file này (thư mục cài đặt VS CODE)
-	"" :    thì compiler thì nó sẽ tìm trong project hiện tại  
Ví dụ #include <stdio.h> hoặc #include “gpio.h”
	copy nội dung của file khác vào mã nguồn của chương trình
Lưu ý: không thể include các file.c được.
b)	Chỉ thị tiền xử lý #define 
Chỉ thị #define là 1 macro dùng để định nghĩa các hằng số, macro, hoặc các đoạn mã thay thế trước khi chương trình biên dịch
Chỉ thị #define có 2 loại: 
-	Loại 1: khai báo 1 dòng
-	Loại 2: khai báo nhiều dòng
Cú pháp của khai báo 1 dòng:
#define name value

Trong đó: 
-	Name: tên đại diện cho giá trị hoặc mã thay thế
-	Value: giá trị hoặc đoạn mã thay thế cho name
Ví dụ: #define SIZE 20
Cú pháp của khai báo nhiều dòng:
#define CREATE_FUNC (name, cmd)                \
Void name()                                                          \
{                                                                            \
   Printf(cmd);                                                       \
}
CREATE_FUNC(test1, “This is function 1\n”);

c)	Chỉ thị tiền xử lý #undef
Chỉ thị #undef dùng để hủy định nghĩa của 1 macro đã được định nghĩa trước đó bằng #define 
Vì khi đã define 1 biến là SIZE có giá trị là 20 rồi, thì trong chương trình ta sẽ không thế thay đổi giá trị cúa SIZE thành giá trị khác nữa => phải dùng #undef sau đó #define lại.
d)	Chỉ thị biên dịch có điều kiện
Chỉ thị tiền xử lý #if, #elif, #else
-	#if sử dụng để bắt đầu một điều kiện tiền xử lý.
-	Nếu điều kiện trong #if là đúng, các dòng mã nguồn sau #if sẽ được biên dịch
-	Nếu sai, các dòng mã nguồn sẽ bị bỏ qua đến khi gặp #endif
-	#elif dùng để thêm một điều kiện mới khi điều kiện trước đó trong #if hoặc #elif là sai
-	#else dùng khi không có điều kiện nào ở trên đúng.
Ví dụ: Nếu có 1 source code khai báo sử dụng cho nhiều vi điều khiển khác nhau, thì có thể sử dụng những chỉ thị biên dịch có điều kiện 
#define A 0 
#define B 1
#define C 2

#define SU A
#if SU == A
     Void inNhomA() {printf(“Nhom A\n”);}
#elif SU == B
     Void inNhomB() {printf(“NhomB\n”);}
#endif

Lưu ý: Sự khác nhau với if else thông thường, với ví dụ trên thì nếu thay chỉ thị tiền xử lý điều kiện thành các lệnh điều kiện thông thường thì sẽ bị sai về cấu trúc C
Chỉ thị tiền xử lý #ifdef, #ifndef
-	#ifdef dùng để kiểm tra một macro đã được định nghĩa hay chưa, nếu macro đã được định nghĩa thì mã nguồn sau #ifdef sẽ được biên dịch.
-	#ifndef dùng để kiểm tra một macro đã được định nghĩa hay chưa, nếu macro chưa được định nghĩa thì mã nguồn sau #ifndef sẽ được biên dịch
	thường được ứng dụng để viết thư viện 
	Thực tế thường không include những file.c mà include những file .h (chứa những khai báo, hàm sẽ sử dụng )
Bước 2: compiler 
Sau khi chương trình đi qua quá trình tiền xử lý dữ liệu thì sẽ thực hiện quá trình compiler. Chuyển các file .i thành các file.s (file hợp ngữ assembly) 
Sử dụng câu lệnh sau để chuyển đổi
gcc -S main.c -o main.s

Bước 3: Assembler
Từ file assembly (file.s) sẽ chuyển thành file .o (obj) chứa những mã nhị phân mà máy tính có thể hiểu được (cũng có lệnh riêng)
Assembly như là 1 ngôn ngữ trung gian để chuyển thành ngôn ngữ bậc cao cho máy tính
Sử dụng câu lệnh để chuyển đổi
gcc –c main.c –o main.c

Sau khi đã chuyển đổi thanh file.o rồi thì vẫn chưa thể run code được, còn phải thực hiện thao tác cuối cùng đó là linker
Bước 4: linker
Linker là quá trình liên kết tất cả file .o lại để thành file .exe để máy có thể run được 
Thực hiện cú pháp sau trên terminal 
gcc main.o -o name

Tóm lại
Khi run file chương trình file.c hoặc file.h thì compiler nó sẽ tạo ra file .exe. file.exe này tượng trưng cho việc chương trình sẽ chạy qua 4 quá trình: Tiền xử lý preprocessor -> Compiler ->  Assembler  -> Linker 

BÀI 2: THƯ VIỆN STDARG – ASSERT
2.1. thư viện stdarg
-	Cung cấp các phương thức để làm việc với các hàm có số lượng input parameter không cố định.
-	Giống với macro, cung cấp các hàm, các macro, có thể làm việc với lượng hàm không xác định
-	Các hàm như printf và scanf là ví dụ điển hình 
Các câu lệnh trong thư viện stdarg
-	va_list: là một kiểu dữ liệu để đại diện cho danh sách các đối số biến đổi.
-	Cú pháp
typedef char* va_list

-	va_start: Bắt đầu một danh sách đối số biến đổi. Nó cần được gọi trước khi truy cập các đối số biến đổi đầu tiên.
-	Cú pháp:
va_start(va_list args, label)

-	va_arg: Truy cập một đối số trong danh sách. Hàm này nhận một đối số của kiểu được xác định bởi tham số thứ hai
-	cú pháp
va_arg(va_list args, <data_type>)

-	va_end: Kết thúc việc sử dụng danh sách đối số biến đổi. Nó cần được gọi trước khi kết thúc hàm.
-	Cú pháp
va_end(va_list args)

-	va_copy: (C99 trở lên mới có): sao chép nội dung từ 1 biến va_list sang 1 biến khác
-	cú pháp
va_copy(va_list args1, va_list args2)

Ví dụ 1: có quy định số lượng tham số
Void test (int count,…)
{
   va_list args; 
   va_start(args, count);
   printf(“value1: %d\n”, va_arg(args, int));
   va_end(args);
}
Int main(void)
{
    Test(1,2);
}

Trong ví dụ trên hàm test có các tham số là tên count (số lượng phần tử), và “…” tượng trưng cho các tham số không xác định
Trong hàm main gọi hàm test (1,2): ý nghĩa là có 1 phần tử đó là số 2 
Kết quả sẽ in ra là value1: 2
Ví dụ 2: không cần quy định số lượng tham số
#define tong(…)          sum(__VA_ARGS__, 0)
Int sum(int count,…)
{
   va_list args; 
   va_start(args, count);
   int result = count;
   int value;
   while((value = va_arg(args, int)) != 0)
   { result += value;}
   va_end(args);
}
Int main(void)
{
    printf(“value1: %d\n”, tong(4,1,2,3,0,1);
}

__VA_ARGS__ : là một phần trong cú pháp của variadic macros, cho phép truyền một số lượng tham số không cố định vào trong một macro.
Kết quả sẽ là 4+1+2+3, vì có số 0 chặn nên sẽ không tính các số ở sau số 0
2.2. thư viện assert
-	Cung cấp macro assert. 
-	Macro này được sử dụng để kiểm tra một điều kiện. 
-	Nếu điều kiện đúng (true), không có gì xảy ra và chương trình tiếp tục thực thi.
-	Nếu điều kiện sai (false), chương trình dừng lại và thông báo một thông điệp lỗi.
-	Dùng trong debug, dùng #define NDEBUG để tắt debug
Cú pháp: 
assert(condition && condition2);

●	Dâu hiệu trong các file: assert_param();: nó là những macro thay thế cho các câu lệnh assert 
Ví dụ 1: Dùng assert để thay thế cho if-else
#include <stdio.h>
#include <assert.h>

int main() {
    int x = 5;

    assert(x == 5);

    // Chương trình sẽ tiếp tục thực thi nếu điều kiện là đúng.
    printf("X is: %d", x);
    
    return 0;
}


Ví dụ 2: dùng macro trong assert thay thế cho assert
// Macro dùng để debug
#define LOG(condition, cmd) assert(condition && #cmd)

BÀI 3: BIT MASK
Bitmask là một kỹ thuật sử dụng các bit để lưu trữ và thao tác với các cờ (flags) hoặc trạng thái. Có thể sử dụng bitmask để đặt, xóa và kiểm tra trạng thái của các bit cụ thể trong một từ (word).
Bitmask thường được sử dụng để tối ưu hóa bộ nhớ, thực hiện các phép toán logic trên một cụm bit, và quản lý các trạng thái, quyền truy cập, hoặc các thuộc tính khác của một đối tượng.
3.1.	Lí do nên dùng bit mask 
Khi khai báo các biến với các kiểu dữ liệu int, uint, char,….thì sẽ chiếm bộ nhớ lớn 
●	// int, int32_t, uint32_t   : 4 byte = 32 bit
●	// int8_t, uint8_t          : 1 byte = 8 bit
●	// int16_t, uint16_t        : 2 byte = 16 bit
Nhưng nếu sử dụng bit mask thì ta có thể lưu trữ trạng thái của từng biến (0, 1) trong các bit => điều này sẽ giúp giảm thiểu được số lượng bộ nhớ hơn 
3.2.	Các loại toán tử bitwise
a)	NOT bitwise
Dùng để thực hiện phép NOT bitwise trên từng bit của một số. Kết quả là bit đảo ngược của số đó.
int result = ~num ;

b)	AND bitwise
Dùng để thực hiện phép AND bitwise giữa từng cặp bit của hai số. Kết quả là 1 nếu cả hai bit tương ứng đều là 1, ngược lại là 0.
int result = num1 & num2;

c)	OR bitwise
Dùng để thực hiện phép OR bitwise giữa từng cặp bit của hai số. Kết quả là 1 nếu có hơn một bit tương ứng là 1.
int result = num1 | num2;

d)	XOR bitwise
Dùng để thực hiện phép XOR bitwise giữa từng cặp bit của hai số. Kết quả là 1 nếu chỉ có một bit tương ứng là 1.
int result = num1 ^ num2;

 
e)	Shift left và Shift right bitwise
Dùng để di chuyển bit sang trái hoặc sang phải.
Trong trường hợp <<, các bit ở bên phải sẽ được dịch sang trái, và các bit trái cùng sẽ được đặt giá trị 0.
Trong trường hợp >>, các bit ở bên trái sẽ được dịch sang phải, và các bit phải cùng sẽ được đặt giá trị 0 hoặc 1 tùy thuộc vào giá trị của bit cao nhất (bit dấu).
int resultLeftShift = num << shiftAmount;
int resultRightShift = num >> shiftAmount;


Ví dụ: 
10010010 << 2 => 01001000
10010010 >> 5 => 00000100
BÀI 4: POINTER
Trong ngôn ngữ lập trình C, con trỏ (pointer) là một biến chứa địa chỉ bộ nhớ của một đối tượng khác (biến, mảng, hàm). Việc sử dụng con trỏ giúp chúng ta thực hiện các thao tác trên bộ nhớ một cách linh hoạt hơn. Dưới đây là một số khái niệm cơ bản về con trỏ trong C:
4.1. khai báo con trỏ, giá trị và địa chỉ của con trỏ
Khai báo con trỏ
Int test = 8;	Address: 0x01
Value:	0
Ptr_x chứa địa chỉ của test
int *ptr_x = &test;	Address: 0xf1
Value:	0x01

Lấy giá trị của địa chỉ ptr_x gán cho y => dùng dải tham chiếu
int y = *ptr_x;   // y sẽ bằng giá trị của x (dereference)	Address: 0xa1
Value: 8

Ví dụ
#include <stdio.h>

int test = 0;
int *ptr = &test;

int main(int argc, char const *argv[]) {
    printf("Gia tri cua con tro: %d\n", *ptr); // Giá trị của test
    printf("Dia chi ma con tro tro toi: %p\n", ptr); // Địa chỉ của test
    printf("Dia chi cua chinh con tro: %p\n", &ptr); // Địa chỉ của ptr
    return 0;
}


kích thước con trỏ 
Kích thước của con trỏ phụ thuộc vào kiến trúc máy tính và trình biên dịch hoặc kiến trúc vi xử lý.
Ví dụ:
Kiến trúc máy tính là hệ điều hành 64 bit => 8 bytes, 32 bit => 4 bytes
Kích thước con trỏ mặc định là số bytes mà hệ điều hành có
Nếu làm trên vxl: 
Arduino 8 bit => 1 bytes
STM32 32 bit => 4 bytes 
ESP32 32 bit  => 4 bytes
Lưu ý 1:
 không thể sử dụng con trỏ có kiểu dữ liệu 1 để lưu trữ cho địa chỉ 1 biến có kiểu dữ liệu khác và phải sử dụng kiểu dữ liệu cho con trỏ và biến giống nhau  
 Ví dụ:
double a = 3.14;
Int *ptr = &a;

Vì biến a được khai báo kiểu double có kích thước là 8 byte. Nhưng con trỏ thì là kiểu int 4 byte nên khi mà con trỏ lưu trữ địa chỉ cho biến a thì nó bị khuyết mất 4 byte và kết quả sẽ bị sai 
double a = 3.14;
double *ptr = &a;

Lưu ý 2: khi con trỏ là 1 mảng
Bản chất của mảng là các ô địa chỉ liền kề nhau, nên mỗi phân tử trong mảng sẽ chiếm 8 byte (đối với kiểu dữ liệu double)
Nên khi mà khai báo con trỏ cho mảng 
Thì con trỏ chỉ lấy địa chỉ đầu tiên trong mảng mà thôi
Ví dụ 
double arr[] = {1,2,3};         // 1: 0xa0 -> 0xa7, 2: 0xa8 -> 0xaf,... : cap phat 8   						byte cho moi phan tu 
char *ptr2 = arr;

Kiểu dữ liệu con trỏ (char) sẽ quyết định bước nhảy 
Với kiểu char là 1 byte=> nên khi + 1 lên thì tự động nó sẽ tăng lên 1 byte thôi
=> ptr2 = 0xa0
=> ptr2 + 1= 0xa1		
=> ptr2 + 1 = 0xa2
=> SAI
Đồng bộ 2 kiểu dữ liệu lại sao cho giống nhau
double arr[] = {1,2,3};         // 1: 0xa0 -> 0xa7, 2: 0xa8 -> 0xaf,... : cap phat 8   						byte cho moi phan tu 
double *ptr2 = arr;
Lúc này, Kiểu dữ liệu con trỏ (double) sẽ quyết định bước nhảy 
Với kiểu char là 8 byte=> nên khi + 1 lên thì tự động nó sẽ tăng lên 8 byte thôi
=> ptr2 = 0xa0		tuong ứng với 1
=> ptr2 + 1= 0xa8		tương ứng với 2
=> ptr2 + 1 = 0xb0		tương ứng với 3
=> ĐÚNG
Bản chất của của số 1 là 1* sizeof(<data type>)
4.2. con trỏ void (void pointer)
Void pointer thường dùng để trỏ đến tới bất kỳ địa chỉ nào mà không cần biết tới kiểu dữ liệu của giá trị tại địa chỉ đó.
Cú pháp:
void *ptr_void;

Ví dụ
Void *ptr;
Int a = 10;
Ptr = &a;
Printf(“addr: %p – value: %d\n”, ptr, *ptr);

Muốn lấy địa chỉ thì dùng %p 
Nếu muốn lấy giá trị mà dùng *ptr thì sẽ bị lỗi. Vì Ở đây con trỏ void đang lấy giá trị tại địa chỉ của int a (kiểu số nguyên). Kiểu dữ liệu này sẽ quyết định bao nhiêu byte mình đọc ra
Nhưng kiểu void thì không quan tâm đến bất kì loại dữ liệu nào, nên khi mà chỉ dùng *ptr thì compiler sẽ không biết được mình đang muốn sử dụng kiểu dữ liệu gì (cụ thể hơn là không biết mình muốn truy cập bao nhiêu byte trong tổng số kiểu dữ liệu của biến (TH này là 4 byte)) => lỗi 
Void *ptr;
Int a = 10;
Ptr = &a;
Printf(“addr: %p – value: %d\n”, ptr, *(int *) ptr);
a)	Khai báo con trỏ void là 1 mảng
Ví dụ
Void *ptr;
Char arr[] = “hello”;
Ptr = arr;

For( size_t i = 0; i < (sizeof(arr)/sizeof(arr[0]); i++)
{
     Printf(“addr: %p – value: %c\n”, ptr, *(char *) (ptr+i));
}

b)	Khai báo con trỏ void như 1 mảng
Cú pháp
Void *ptr1[] = {&a,&b,&c, arr};

Từng phần tử bên trong con trỏ void là các địa chỉ đến đối tượng khác
Ưu nhược điểm của con trỏ hàm (void pointer)
Ưu điểm:
●	Không cần phải khai báo biến con trỏ cho từng biến => làm to bộ nhớ RAM
●	Chỉ cần khai báo 1 con trỏ void, nó có trỏ đến bất kì biến nào cx được, chỉ tốn 1 lần cấp phát cho con trỏ void thôi (1 vùng nhớ), 
●	Tại vùng nhớ này có thể thao tác với bát kì kiểu dữ liệu nào cx được
Nhược điểm:
●	Muốn đọc được dữ liệu phải ép kiểu về để đồng bộ dữ liệu
4.3. con trỏ hàm
Pointer to function (con trỏ hàm) là một biến mà giữ địa chỉ của một hàm. Có nghĩa là, nó trỏ đến vùng nhớ trong bộ nhớ chứa mã máy của hàm được định nghĩa trong chương trình.
Trong ngôn ngữ lập trình C, con trỏ hàm cho phép bạn truyền một hàm như là một đối số cho một hàm khác, lưu trữ địa chỉ của hàm trong một cấu trúc dữ liệu, hoặc thậm chí truyền hàm như một giá trị trả về từ một hàm khác.
Cú pháp
<return_type> (* func_pointer)(<data_type_1>, <data_type_2>);

Lưu ý khi khai báo hàm
-	kiểu trả về: Nếu là kiểu int, double, char thì phải có return: giá trị trả về
-	Tham số truyền vào
-	Khi khai báo 1 hàm, thi sẽ tự động cấp phát vùng nhớ cho hàm này. Thì để mà thao tác trên địa chỉ của các hàm này, thì mình phải khai báo ra 1 con trỏ hàm. 
-	Khi mà các hàm func1 có kiểu trả về là kiểu void, không có tham số truyền vào => khai báo con trỏ hàm tương tự như vậy 
-	Thì khi mà khai báo con trỏ hàm, thì con trỏ hàm này chỉ lưu trữ địa chỉ của những hàm tương ứng với nó thôi, tức là những hàm giống y hệt nó
a)	Biến con trỏ hàm
Ví dụ:
Void func1()
{printf(“This is function 1”);}
Void func2(int a, double b, char c)
{printf(“This is function 2”);}
Void func(int a, int b)
{printf(“This is function 3”);}

Main()
{
    void(*ptr)();                       => con trỏ này chỉ lưu trữ địa chỉ của hàm func1
    ptr = func1;                        => gán địa chi của hàm
    ptr();                                   => thực thi con trỏ hàm
    int (*ptr1)(int, double, char);    => con trỏ này chỉ lưu trũ địa chỉ hàm func2
    ptr1 = func2;                        => gán địa chi của hàm
    ptr1(4, 4.8, ‘a’);                   => thực thi con trỏ hàm
    void (*ptr2)(int, int);             => còn con trỏ này thì lưu trữ địa chỉ hàm func3
    ptr2 = func3;                        => gán địa chi của hàm
    ptr2(3,4);                              => thực thi con trỏ hàm
    
    return 0;
}

b)	Con trỏ hàm hoạt động như 1 tham số truyền vào của hàm
Ví dụ
Void tong(int a, int b)
{printf(“%d + %d = \n”, a,b, a+b);}

Void compute(void (*ptr)(int, int), int a, int b)
{
    Ptr(a,b);
}

Main()
{
    Int a= 20, b= 30;
    Compute(tong, a,b);
}

c)	Mảng con trỏ hàm
Void tong(int a, int b)
{printf(“%d + %d = \n”, a,b, a+b);}

Main()
{
    Int a= 20, b= 30;
    void((*tinhtoan[])(int, int) = {&tong});
    tinhtoan[0](a,b);
    return 0;
}

Lưu ý:
Việc sử dụng con trỏ hàm khác với hàm thông thường là:
Trong compiler, thì chương trình sẽ trải qua 2 giai đoạn, 
- giai đoạn 1 là biên dịch (compile time), 
- giai đoạn 2 là bắt đầu chạy chương trình (run time)
Khi mà thao tác với 1 hàm thông thường (tong(a,b)) thì nó sẽ xảy ra ở quá trình biên dịch (compile time), những hàm này đã khai báo sãn rồi, và nó chỉ biên dịch ra thôi
Còn những con trỏ hàm thì nó xảy ra trong quá trình (run time), khiến cho nó linh hoạt hơn. (trong quá trình chạy có thể thay đổi đột ngột được ),   giống scanf 
Ưu nhược điểm của con trỏ hàm
Ưu điểm: Linh hoạt hơn các hàm thông thường do là con trỏ hàm xảy ra ở quá trình runtime, còn các hàm thông thường thì xảy ở qua trình biên dịch
4.4. con trỏ hằng (pointer to const)
Là cách định nghĩa một con trỏ không thể thay đổi giá trị tại địa chỉ mà nó trỏ đến thông qua dereference nhưng giá trị tại địa chỉ đó có thể thay đổi.
READ ONLY
Cú pháp: 
int const *ptr_const; 
const int *ptr_const;

4.5. hằng con trỏ (const to pointer)
Định nghĩa một con trỏ mà giá trị nó trỏ đến (địa chỉ ) không thể thay đổi. Tức là khi con trỏ này được khởi tạo thì nó sẽ không thể trỏ tới địa chỉ khác.
Chỉ trỏ đến 1 địa chỉ duy nhất xuyên suốt chương trình. Tại giá trị mà nó trỏ tới, mình có thể đọc được , ghi được (tác động được đến nó)
Cú pháp
int *const const_ptr = &value;

4.6. con trỏ NULL
Null Pointer là một con trỏ không trỏ đến bất kỳ đối tượng hoặc vùng nhớ cụ thể nào. Trong ngôn ngữ lập trình C, một con trỏ có thể được gán giá trị NULL để biểu diễn trạng thái null, C++ (NULL, nullptr).
Sử dụng null pointer thường hữu ích để kiểm tra xem một con trỏ đã được khởi tạo và có trỏ đến một vùng nhớ hợp lệ chưa. Tránh dereferencing (sử dụng giá trị mà con trỏ trỏ đến) một null pointer là quan trọng để tránh lỗi chương trình.
4.7. pointer to pointer
Con trỏ đến con trỏ (Pointer to Pointer) là một kiểu dữ liệu trong ngôn ngữ lập trình cho phép bạn lưu trữ địa chỉ của một con trỏ. Con trỏ đến con trỏ cung cấp một cấp bậc trỏ mới, cho phép bạn thay đổi giá trị của con trỏ gốc. Cấp bậc này có thể hữu ích trong nhiều tình huống, đặc biệt là khi bạn làm việc với các hàm cần thay đổi giá trị của con trỏ.
●	Int *ptr = NULL;		đây là con trỏ cấp 1: lưu trữ địa chỉ của 1 biến
●	Để mà thao tác đến địa chỉ của con trỏ cấp 1 này, ngoài việc dùng
●	Int *ptr1 = &ptr;		
●	 thì có thể dùng con trỏ có cấp cao hơn.
●	Int **ptr2 = &ptr;		con trỏ cấp 2: lưu địa chỉ của con trỏ cấp 1
●	Int ***ptr3 = &ptr2		con trỏ cấp 3 lưu địa chỉ của con trỏ cấp 2
BÀI 5: STORAGE CLASSES
5.1. extern
Đặt vấn đề:
Giả sử ở file test.c có 1 biến a bất kỳ, nếu như file khác muốn sử dụng biến này, ngoài việc sử dụng #include thì liệu có cách nào khác không ?
Tại sao không sử dụng #include ?
Trả lời:
Khi có file test1.c như trên, có khai báo biến a = 10
Nếu muốn sử dụng biến a trong file khác, cụ thể là file main.c thì ta phải include file test1.c trong file main để có thể sử dụng biến a. Bản chất của việc, tức là nó sẽ copy toàn bộ các câu lệnh có trong file test1.c vào trong file main.i. lúc này thì file main,c có thể thao tác được các biến đã được khai báo trong file test1.c. 
Đây là cách thông thường hay làm, nhưng cách này có 1 nhước điểm. Đó là 
-  Thông thường thì không có ai include file.c cả mà thường thì sẽ include file .h vì các file.c thường sẽ có hàm main trong đó. Mà trong project thì chỉ duy nhất 1 hàm main thôi, nên nếu trường hợp đó xảy ra thì sẽ gây ra lỗi
-	việc include nhiều file.c nhiều thì như đã nói nó sẽ phải copy tất cả các câu lệnh vào trong mã nguồn. Trong trường hợp nếu chỉ muốn sử dụng biến a, không sử dụng biến b thì sao??
-	=> việc này buộc chương trình phải cấp phát đủ cho biến a và biến b mặc dù việc cấp phát cho biến b là không cần thiết => gây tốn bộ nhớ 
=> để tránh việc này xảy ra thì chúng ta sẽ sử dụng từ khóa extern 
-	Dùng từ khóa extern. Việc này giúp cho, không khởi tạo dữ liệu bộ nhớ cho biến a trong main.c nữa , (vì biến a đã được khởi tạo dữ liệu trong file test1.c rồi)
-	Tương tự với hàm cũng vậy, chỉ khai báo tên hàm thôi chứ không cần nội dung của hàm, vì nội dung của hàm đã được khai bảo trong các file .c khác rồi
-	=> nhưng đặc biệt ở chỗ các hàm không cần khai báo extern nhưng vẫn dùng được. Đối với những hàm thì khi khai báo toàn cục như test1 và test2.c thì trong C mặc định là các file khác có thể sử dụng nó luôn
-	Còn biến thì buộc phải khai báo extern
-	Ở đây nếu chỉ dừng lại ở đây mà bấm runcode thì nó sẽ không chạy được. Lí do là vì các file này chưa có liên kết lại với nhau
Để có thể sử dụng extern các file cần phải được liên kết lại với nhau thông qua câu lệnh
gcc main.c test1.c test2.c -o main
Câu lệnh này cx đơn giản chỉ là 1 cách nhanh hơn của tiền xử lý, tạo file.i .s.o linker    bằng cách chạy ngầm 
Cú pháp:
      gcc <tên file1.c> <tên file2.c>…. –o “tên file cần đặt”

khái niệm extern:
Khái niệm Extern trong ngôn ngữ lập trình C được sử dụng để thông báo rằng một biến hoặc hàm đã được khai báo ở một nơi khác trong chương trình hoặc trong một file nguồn khác. Điều này giúp chương trình hiểu rằng biến hoặc hàm đã được định nghĩa và sẽ được sử dụng từ một vị trí khác, giúp quản lý sự liên kết giữa các phần khác nhau của chương trình hoặc giữa các file nguồn.
ứng dung:
●	Viết thư viện
●	Chỉ sử dụng cho biến toàn cục 
5.2. static
Static có thể được sử dụng cho biến cục bộ và cả biến toàn cục
5.2.1 static cục bộ
Khi static được sử dụng với local variables (biến cục bộ - khai báo biến trong một hàm), nó giữ giá trị của biến qua các lần gọi hàm và giữ phạm vi của biến chỉ trong hàm đó.
●	Trong phân vùng BSS thì nó có đặc điểm là 
●	- sau khi kết thúc lần gọi hàm thì nó sẽ không thu hồi lại các địa chỉ đã tạo ra, mà chỉ khi kết thúc toàn bộ chương trình thì nó mới thu hồi phân vùng BSS này. hoặc là tắt VS CODE thì mới thu hồi đi 
●	- Địa chỉ của biến a chỉ được cấp phát 1 lần duy nhất, cấp phát ở lần đầu tiên gọi hàm ra, từ lần gọi hàm thứ 2 trở đi, thì nó sẽ bỏ qua dòng khởi tạo biến static a , đi tới thẳng luôn dòng printf (phạm vi chỉ nằm trong hàm count thôi) 
●	Vì biến static có phạm vi là toàn cục nên chúng ta Có thể tác động tới địa chỉ của biến static để có thể thay đổi giá trị của nó
ứng dụng:
muốn biến nào giữ nguyên giá trị sau mỗi lần gọi hàm thì dùng static cục bộ
5.2.2. static toàn cục
Khi static được sử dụng với global variables ( biến toàn cục - khai báo biến bên ngoài hàm), nó hạn chế phạm vi của biến đó chỉ trong file nguồn hiện tại.
Ứng dụng: dùng để thiết kế các file thư viện.
Đặc điểm:
●	Khi mà khai báo các biến bằng từ khóa static thì nó sẽ bị giới hạn trong file hiện tại mà thôi
●	Ở đây biến a đã được khai báo là static trong file test1.h nên ta không thể nào lấy biến a này 
=> hạn chế phạm vi của đối tượng chỉ được gọi trong file đó thôi (gọi trong file nào thì chỉ sử dụng được trong file đó thôi) (ngay cả từ khóa extern cũng không thể tác động)
5.3. register
Trong ngôn ngữ lập trình C, từ khóa register được sử dụng để chỉ ra ý muốn của lập trình viên rằng một biến được sử dụng thường xuyên và có thể được lưu trữ trong một thanh ghi máy tính, chứ không phải trong bộ nhớ RAM. Việc này nhằm tăng tốc độ truy cập. Tuy nhiên, lưu ý rằng việc sử dụng register chỉ là một đề xuất cho trình biên dịch và không đảm bảo rằng biến sẽ được lưu trữ trong thanh ghi. Trong thực tế, trình biên dịch có thể quyết định không tuân thủ lời đề xuất này.
5.3.1 quá trình thực hiện
 
ALU là bộ xử lý các phép toán số học
Quá trình 
-	(1) Khi khai báo int i = 5 (khai báo static, extern cx vậy) thì nó sẽ lưu giá trị của biến này tại địa chỉ nào đó trong bộ nhớ RAM
-	(2) Từ bộ nhớ RAM nó sẽ dẩy sang các thanh ghi, lưu giá trị của biến i vào trong 1 trong các thanh ghi, thanh ghi nào trống thì nó sẽ lưu vào
-	Từ thanh ghi này thì nó sẽ tác động vào bộ ALU này, trong bộ ALU thì có bộ xử lý tính toán số học và đặc điểm của bộ ALU là nó sẽ nhận dữ liệu từ  thanh ghi thôi, không nhận dữ liệu từ bộ nhớ RAM. 
-	=> Nên muốn lấy dữ liệu để tính toán thì mình phải lưu qua các trung gian là những thanh ghi 
-	Phép ++i cx vậy, thông tin ++ này sẽ được lưu vào trong các thanh ghi nào đó, sau đó gửi thông tin này đến ALU
-	(3) Sau đó, ALU tính toán xong thì nó sẽ trả ngược về thanh ghi
-	(4) thanh ghi sẽ gửi giá trị này về lại địa chỉ của biến 
-	=> 4 giai đoạn
Trên thực tế thì hoàn toàn có thể bỏ qua bộ nhớ RAM này, không muốn biến i lưu trực tiếp trên RAM mà lưu thẳng vào thanh ghi. Để khi mà lưu trên thanh ghi thì sẽ tiết kiệm được 2 bước chuyển giao giữa thanh ghi và RAM
Để làm được việc này thì mình sẽ khai báo register
Điều này giúp cho việc trả về của dữ liệu qua ALU sẽ nhanh hơn so với việc lưu trữ trên RAM. (có thể sử dụng printf để in ra được. Không vấn đề gì )	
5.3.2. tổng kết
●	Thường sử dụng khi mà ưu tiên cho biến đó thực hiện những phép toán số học 
●	Khi mà trình biên dịch thấy sử dụng register nghĩa là nó sẽ không lưu trữ trên RAM mà nó sẽ lưu trữ trực tiếp trên thanh ghi
●	Register sẽ không thể lấy địa chỉ được, không sử dụng con trỏ để trỏ đến các biến register. Vì thanh ghi thì nó sẽ không có địa chỉ. 
●	Register chỉ sử dụng cho những biến cục bộ thôi. Đối với biến toàn cục thì nó sẽ phải tồn tại xuyên suốt chương trình, mà nếu sử dụng register cho biến toàn cục thì nó sẽ chiếm dụng 1 thanh ghi trong số các thanh ghi, mà thanh ghi thì có giới hạn chỉ vài chục cái. Việc chiếm dụng thanh ghi này sẽ làm chậm hiệu suất của chương trình
●	Ngày nay, do đã phát minh ra các vi điều khiển chạy rất nhanh rồi nên bây h người ta ít xài từ khóa register. Do bộ xử lý về sau này rất nhanh và mạnh, nhưng mà nếu sử dụng các dòng vi xử lý xưa cổ thì bộ xử lý của nó sẽ rất chậm, nếu muốn tăng tốc thì sử dụng register vào  
5.4. volatile 
Từ khóa volatile trong ngôn ngữ lập trình C/C++ được sử dụng để báo hiệu cho trình biên dịch rằng một biến có thể thay đổi ngẫu nhiên, ngoài sự kiểm soát của chương trình. Việc này ngăn chặn trình biên dịch tối ưu hóa hoặc xóa bỏ các thao tác trên biến đó, giữ cho các thao tác trên biến được thực hiện như đã được định nghĩa.
Trong lập trình C/C++, khi mà khai báo 1 biến toàn cục. Khi mà khai báo các biến như là 
Int a;
Int b;

Mà lại không sử dụng. Khi chạy chương trình bao nhiêu lần đi nữa, thì a, b không thay đổi. 
Khi đó trình biên dịch có 1 cơ chế, nó thấy biến nào (biến toàn cục), (not biến cục bộ vì khi kết thúc hàm là nó đã bị thu hồi rồi) , những biến nào mà sau khi chạy chương trình nhiều lần, trình biên dịch tháy không có thay đổi thì nó sẽ tự động tối ưu hóa những biến đó đi, tự động xóa những biến đó đi. Mặc dù khai báo vẫn còn nhưng mà nó sẽ hiểu ngầm là không sử dụng những biến này nữa.
Lưu ý từ khóa volatile không thể thực hiện được ở trên vs code mà chỉ có trên phần cứng vi điều khiển mới có 
	Volatile là dùng để ngăn trình biên dịch tối ưu hóa 1 biến nào đó
	Thực tế, khi mà lập trình vi điều khiển thì sẽ có những lúc làm cho các biến thay đổi đột ngột như là Ngắt, … giá trị bị thay đổi đột ngột 
	Khi mà ngắt thì dữ liệu vẫn giữ chứ không mất đi
	Thường ứng dụng cho những việc đọc dữ liệu cảm biến,… 



