# Customize Run and Debug - Flutter

## 1. Intro

Xin chào các bạn! Bài viết hôm nay tiếp tục là một chủ đề về Flutter. 

## 2. Giới thiệu bản thân

Nếu các bạn đã đọc được bài viết trước của mình ở [đây](https://github.com/vanle57/flutter-flavor) thì đã biết mình là ai. Còn nếu chưa (nhưng mà mình khuyên chân thành là các bạn nên đọc bài trước vì bài này có nội dung liên quan đến bài trước đó!) thì mình xin tự giới thiệu lại lần nữa. Mình là Lê Hồng Vân, là dev iOS và mới tự mày mò, tìm hiểu Flutter được nửa năm nay. Trong tương lai, mình dự định sẽ có một bài chia sẻ về quá trình tự học của mình để những ai cũng có mong muốn tự học hỏi như mình sẽ tích luỹ được chút kinh nghiệm cho quá trình tự học của bản thân. Các bạn cùng đón chờ nhé!

Follow me more:
| [![Facebook](https://github.com/vanle57/flutter-customize-run/blob/main/images/facebook.png)](https://www.facebook.com/van.may.750/) |    [![Gmail](https://github.com/vanle57/flutter-customize-run/blob/main/images/google.png)](mailto:hongvan.571996@gmail.com) |  [![Linkedin](https://github.com/vanle57/flutter-customize-run/blob/main/images/linkedin.png)]()   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --- | --- |

## 3. Chuẩn bị

- IDE:
  - VSCode version 1.67.0
  - Android Studio Bumblebee version 2021.1.1 Patch 3
  - XCode version 13.3.1
- Flutter SDK version 2.10.5

## 4. Khát quát về Launch configuration

- VS Code giúp bạn đơn giản hoá việc khởi chạy và debug các cấu hình custom của app. Để làm được điều đó, VS Code sẽ đọc file launch.json nằm trong folder .vscode và việc chúng ta cần làm là viết các cấu hình custom chúng ta muốn vào đấy. Và các cấu hình custom này được gọi là **launch configuration**.
- Khi bạn cài Dart và Flutter extension vào VSCode, nó sẽ đi kèm với 1 trình khởi chạy mặc định. Đó là lý do vì sao bạn vẫn có thể chạy ứng dụng mà không có file launch.json.
- Tóm lại, launch configuration **không phải là** tính năng của Dart hay Flutter, nó là một cấu hình để mở rộng khả năng của VS Code. Nếu các bạn sử dụng Android Studio để build code flutter thì có lẽ bài viết này không dành cho bạn rồi. Ahihi!

## 5. Cấu hình file launch.json

Đầu tiên, mình sẽ hướng dẫn cách tạo file launch.json:

- Bạn vào tab `Run and Debug` và click vào *create a launch.json file*.
  
  ![1](https://github.com/vanle57/flutter-customize-run/blob/main/images/1.png)

- Sau khi click thì bạn sẽ thấy 1 file như thế này
  
  ![2](https://github.com/vanle57/flutter-customize-run/blob/main/images/2.png)

- File có nội dung ban đầu với cấu trúc json như sau:

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "demo_flavor",
            "request": "launch",
            "type": "dart"
        },
        {
            "name": "demo_flavor (profile mode)",
            "request": "launch",
            "type": "dart",
            "flutterMode": "profile"
        },
        {
            "name": "demo_flavor (release mode)",
            "request": "launch",
            "type": "dart",
            "flutterMode": "release"
        }
    ]
}
```

Trong object `configurations` chính là các launch configuration mà các bạn có thể custom. Để mình giải thích về một số thuộc tính của launch configuration nhé!

- name: (bắt buộc có) tên của launch configuration sẽ xuất hiện trong menu xổ xuống của tab Run và Debug.
  
  > Là cái menu này nè!
  
  ![3](https://github.com/vanle57/flutter-customize-run/blob/main/images/3.png)

- request: (bắt buộc có) có 2 loại là launch và attach, để phân biệt giữa chúng thì các bạn đọc thêm tại [đây](https://code.visualstudio.com/docs/editor/debugging#_launch-versus-attach-configurations).

- type: (bắt buộc có) loại debbuger sử dụng

- args: các tham số được truyền vào

- program: file để khởi chạy khi launch debugger

Còn rất nhiều tham số mà bạn có thể tham khảo tại [Launch.json attributes](https://code.visualstudio.com/docs/editor/debugging#_launchjson-attributes) nhưng cơ bản với dart thì chỉ cần chừng đó là đủ rồi.

> Bạn không cần phải quá lo lắng về việc hiểu sâu về các thuộc tính này vì khi các bạn tạo ra file launch.json thì VSCode đã chọn sẵn các thuộc tính phù hợp nhất với mình rồi!

## 6. Customize run and debug with flutter flavors

> Dịch nghĩa tiêu đề ra là **Tuỳ chỉnh trình khởi chạy và gỡ rối với các môi trường của Flutter**. Nghe khá khoai nên mình xin phép giữ tiếng Anh cho tiêu đề.

Về Flutter Flavors, các bạn có thể tham khảo lại bài viết trước của mình tại [link này](https://github.com/vanle57/flutter-flavor)

Mình sẽ define 3 launch configuration tương ứng với 3 flavor là dev, staging và product.

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            // 1   
            "name": "dev",
            // 2
            "request": "launch",
            // 3
            "type": "dart",
             // 4
            "args": ["--flavor", "dev"]
        },
        {
            "name": "staging",
            "request": "launch",
            "type": "dart",
            "args": ["--flavor", "staging"]
        },
        {
            "name": "product",
            "request": "launch",
            "type": "dart",
            "args": ["--flavor", "product"]
        }
    ]
}
```

***Giải thích một chút:***

- 1: Mình chọn cách đặt tên theo tên flavor cho dễ phân biệt

- 2 và 3: *request* và *type* sẽ được giữ nguyên theo đề xuất của VS Code

- 4: Chúng ta sử dụng tham số là `--flavor`  với value là các flavor tương ứng mà mình đã config ở [bài trước](https://github.com/vanle57/flutter-flavor). Các bạn có thắc mắc vì sao tham số là `--flavor` không? Ở đây chúng ta sẽ **pass những argument vào câu lệnh `flutter run`**. Như hướng dẫn ở [phần thực thi](https://github.com/vanle57/flutter-flavor#6-th%E1%BB%B1c-thi), câu lệnh chúng ta sẽ thực hiện khi run app Flutter với flavor là `flutter run --flavor {tên flavor tương ứng}`.

## 7. Thực thi

Tới bước này, bạn đã hoàn thành mong muốn là build được các flavor bằng nút build của IDE mà không cần chạy lệnh rồi đó!

Thử chọn từng launch configuration trên `Run Menu` và bấm nút thôi!

![4](https://github.com/vanle57/flutter-customize-run/blob/main/images/4.png)

****Kết quả:**** Bạn có thể thấy 3 cái app với 3 tên khác nhau tương ứng với các flavor do mình đã tạo ở bước trước đó!

<table width="100%">
  <tr>
    <th>iOS</th>
    <th>Android</th>
  <tr>
    <td width="50%"><img src="https://github.com/vanle57/flutter-customize-run/blob/main/images/5.png"></td>
    <td width="50%"><img src="https://github.com/vanle57/flutter-customize-run/blob/main/images/6.png"></td>
  </tr>
</table>

#### [Demo source code](https://github.com/vanle57/flutter-customize-run/tree/main/demo%20source%20code/demo_flavor)

## 8. Tạm kết

Qua 2 bài viết của mình, bạn đã biết cách

- Cấu hình các flavor cho Flutter.

- Sử dụng launch configuration để custom run và debug theo ý muốn của mình.

Có lẽ bạn sẽ cảm thấy còn thiếu thiếu gì đó về flavor. Chúng ta đã có những app name khác nhau, có những application id (android) hay bundle identifier (iOS) khác nhau và tương ứng với từng flavor nhưng còn những đặc trưng nhất của chúng là api url, key service thì sao? Phải làm như thế nào để định nghĩa mỗi api url riêng cho từng flavor? Vậy thì bạn cần phải xem tiếp bài viết sau của mình ở [đây](https://github.com/vanle57/flutter-method-channel). Hoặc bạn cũng có thể xem thêm cách mình ứng dụng launch configuration ở [bài này]().

Cảm ơn các bạn đã theo dõi và hẹn gặp lại!

#### Tài liệu tham khảo:

- [How to run a Flutter app with arguments in VS Code with launch configuration | Sarunw](https://sarunw.com/posts/how-to-run-flutter-app-with-arguments-in-vscode-with-launch-configuration/#what-is-a-launch-configuration)

- [Debugging in Visual Studio Code](https://code.visualstudio.com/docs/editor/debugging)

- [Launch Configuration - Dart Code - Dart & Flutter support for Visual Studio Code](https://dartcode.org/docs/launch-configuration/)
