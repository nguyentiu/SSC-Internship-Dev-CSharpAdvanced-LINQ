# SSC-Internship-Dev-CSharpAdvanced-LINQ
# Hướng Dẫn về LINQ trong C#
## 1. Định nghĩa
LINQ (Language Integrated Query) là một thành phần mạnh mẽ trong C# giúp bạn truy vấn các nguồn dữ liệu khác nhau như Collections, Databases, XML, v.v., theo cách thống nhất và đơn giản. LINQ tích hợp khả năng truy vấn trực tiếp vào ngôn ngữ lập trình C#, giúp bạn viết các câu truy vấn một cách dễ dàng và linh hoạt hơn.

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Sử dụng LINQ để lấy các số chẵn
var evenNumbers = from number in numbers
                  where number % 2 == 0
                  select number;

foreach (var num in evenNumbers)
{
    Console.WriteLine(num); // Output: 2, 4
}
```
## 2. Mệnh đề trong LINQ
LINQ có một số mệnh đề cơ bản tương tự như các câu lệnh SQL:

- from: Xác định nguồn dữ liệu.
- where: Lọc dữ liệu dựa trên điều kiện.
- select: Xác định kết quả trả về.
Ví dụ:

```csharp
string[] names = { "John", "Jane", "Doe", "Daisy" };

// Truy vấn các tên bắt đầu với chữ "D"
var query = from name in names
            where name.StartsWith("D")
            select name;

foreach (var name in query)
{
    Console.WriteLine(name); // Output: Doe, Daisy
}
```
## 3. Các cách để viết query LINQ
Có hai cách phổ biến để viết câu truy vấn LINQ:

### a. Query Syntax: Sử dụng các từ khóa như SQL.

```csharp
int[] numbers = { 5, 10, 15, 20 };

// Query syntax
var query = from num in numbers
            where num > 10
            select num;
```
### b. Method Syntax: Sử dụng các phương thức mở rộng (extension methods).

```csharp
// Method syntax
var methodQuery = numbers.Where(num => num > 10);
```
## 4. Lambda Expressions trong LINQ
Lambda Expressions được sử dụng rộng rãi trong LINQ để viết các câu truy vấn ngắn gọn và hiệu quả.

```csharp
var evenNumbers = numbers.Where(n => n % 2 == 0).ToList();

evenNumbers.ForEach(n => Console.WriteLine(n)); // Output: 10, 20
```
## 5. Sorting: OrderBy, OrderByDescending
Sắp xếp các phần tử trong danh sách sử dụng OrderBy và OrderByDescending.

```csharp
string[] fruits = { "Apple", "Banana", "Mango", "Orange" };

// Sắp xếp theo thứ tự bảng chữ cái
var sortedFruits = fruits.OrderBy(fruit => fruit);

foreach (var fruit in sortedFruits)
{
    Console.WriteLine(fruit); // Output: Apple, Banana, Mango, Orange
}

// Sắp xếp ngược lại
var sortedDescending = fruits.OrderByDescending(fruit => fruit);

foreach (var fruit in sortedDescending)
{
    Console.WriteLine(fruit); // Output: Orange, Mango, Banana, Apple
}
```
## 6. Tạo ra 1 object mới trong Select
Bạn có thể tạo ra một đối tượng mới từ các dữ liệu truy vấn được.

```csharp
var students = new[]
{
    new { Name = "John", Age = 18 },
    new { Name = "Jane", Age = 20 }
};

var studentInfo = students.Select(s => new { FullName = s.Name, AgeInYears = s.Age });

foreach (var info in studentInfo)
{
    Console.WriteLine($"Name: {info.FullName}, Age: {info.AgeInYears}");
    // Output: Name: John, Age: 18
    //         Name: Jane, Age: 20
}
```
## 7. Grouping: GroupBy
Grouping cho phép bạn nhóm các phần tử có cùng giá trị.

```csharp
var people = new[]
{
    new { Name = "John", Age = 18 },
    new { Name = "Jane", Age = 18 },
    new { Name = "Tom", Age = 20 }
};

// Nhóm theo độ tuổi
var groupedByAge = people.GroupBy(p => p.Age);

foreach (var group in groupedByAge)
{
    Console.WriteLine($"Age: {group.Key}");
    foreach (var person in group)
    {
        Console.WriteLine($"- {person.Name}");
        // Output: Age: 18
        //         - John
        //         - Jane
        //         Age: 20
        //         - Tom
    }
}
```
## 8. All, Any
- All: Kiểm tra xem tất cả các phần tử có thỏa mãn điều kiện.
- Any: Kiểm tra xem có phần tử nào thỏa mãn điều kiện không.
```csharp
int[] numbers = { 2, 4, 6, 8 };

// Kiểm tra nếu tất cả các số là số chẵn
bool allEven = numbers.All(n => n % 2 == 0); // Output: True

// Kiểm tra nếu có số lẻ
bool hasOdd = numbers.Any(n => n % 2 != 0); // Output: False
```
## 9. Element: First, FirstOrDefault, Single, SingleOrDefault
- `First`: Lấy phần tử đầu tiên.
- `FirstOrDefault`: Lấy phần tử đầu tiên hoặc giá trị mặc định nếu không có phần tử nào.
- `Single`: Lấy phần tử duy nhất.
- `SingleOrDefault`: Lấy phần tử duy nhất hoặc giá trị mặc định.
```csharp
string[] names = { "John", "Jane", "Doe" };

// Lấy phần tử đầu tiên
string first = names.First(); // Output: John

// Lấy phần tử đầu tiên hoặc giá trị mặc định
string firstOrDefault = names.FirstOrDefault(n => n == "Tom"); // Output: null

// Lấy phần tử duy nhất
string single = names.Single(n => n == "Jane"); // Output: Jane
```
## 10. Partitioning: Skip, Take
- `Skip`: Bỏ qua một số phần tử đầu tiên.
- `Take`: Lấy một số phần tử đầu tiên.
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

// Bỏ qua 2 phần tử đầu tiên và lấy 3 phần tử tiếp theo
var subset = numbers.Skip(2).Take(3);

foreach (var num in subset)
{
    Console.WriteLine(num); // Output: 3, 4, 5
}
```
## 11. Một số hàm phổ biến trong LINQ
- `Count`: Đếm số phần tử.
- `Sum`: Tính tổng.
- `Average`: Tính giá trị trung bình.
- `Max, Min`: Tìm giá trị lớn nhất, nhỏ nhất.
```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

int count = numbers.Count(); // Output: 5
int sum = numbers.Sum(); // Output: 15
double average = numbers.Average(); // Output: 3
int max = numbers.Max(); // Output: 5
int min = numbers.Min(); // Output: 1
```
# Kết luận
LINQ là một công cụ mạnh mẽ trong C# giúp đơn giản hóa việc truy vấn dữ liệu và xử lý các bộ sưu tập. Qua blog này, bạn đã tìm hiểu các khái niệm cơ bản của LINQ, các cách viết truy vấn, và một số hàm phổ biến trong LINQ. LINQ giúp bạn viết mã ngắn gọn hơn, dễ hiểu hơn và dễ bảo trì hơn.
# Nguồn tham khảo
- https://viblo.asia/p/linq-trong-c-6J3ZgpgxlmB
