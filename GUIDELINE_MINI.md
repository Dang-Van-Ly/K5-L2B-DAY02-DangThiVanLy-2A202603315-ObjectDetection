# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp


| Lớp    | Định nghĩa của bạn                                                                                                                                                             | Ví dụ/điểm phân biệt                                                                                                                                                 |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `car`   | Xe con cá nhân hoặc xe nhỏ chở người, thân thấp, không phải xe tải/xe buýt/xe van. Bao gồm sedan, hatchback, SUV, taxi và xe bán tải nhỏ nếu trông như xe con. | Khác`truck` vì không có thùng hàng rõ ràng; khác `bus` vì nhỏ hơn và không là xe chở khách tuyến; khác `van` vì không có thân cao/thùng dạng van. |
| `truck` | Xe tải chở hàng, xe container, xe đầu kéo hoặc phương tiện vận tải có thùng/cabin rõ ràng.                                                                          | Dễ nhận biết nhờ thùng hàng hoặc cabin lớn; không dùng cho xe bán tải/xe gia đình nhỏ.                                                                      |
| `bus`   | Xe buýt hoặc minibus chở khách theo tuyến, thường lớn và dài hơn xe con/van.                                                                                             | Khác`van` vì là phương tiện khách tuyến lớn, có hình dạng dài, nhiều cửa/ghế; khác `car` vì kích thước rõ ràng lớn hơn.                           |
| `van`   | Xe van/minivan, xe chở hàng hoặc chở người có thân cao, đa dụng.                                                                                                          | Điểm phân biệt với`bus` là nhỏ hơn, không phải xe khách tuyến quy mô lớn; với `car` là thân cao hơn và hình dạng xe vận tải/đa dụng.              |

## Quy tắc chung

- Box bám sát vật thể nghĩa là: vẽ sát mép ngoài phần xe nhìn thấy, không bao gồm mặt đường, vạch kẻ, trời, bóng, hay vật thể lân cận; chỉ giữ đúng phần thân xe cần thiết để nhận diện lớp.
- Vật thể bị che khuất: nếu phần xe còn nhìn thấy đủ để xác định lớp và vẽ box, vẫn gán box cho phần còn thấy; nếu bị che gần như toàn bộ mà không xác định chắc lớp thì không đoán.
- Vật thể bị cắt bởi rìa ảnh: chỉ vẽ phần còn nằm trong khung hình, không suy đoán phần ngoài ảnh. Nếu còn đủ để nhận diện, vẫn gán box chỉ cho phần nhìn thấy.
- Vật thể rất nhỏ/mơ hồ: nếu quá nhỏ hoặc mờ đến mức không chắc chắn `car`/`truck`/`bus`/`van`, không tự đoán. Ghi lại và xét lại hoặc hỏi giảng viên nếu cần.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ


| Ảnh              | Tình huống                                                                         | Quyết định cuối                                                                                                             | Lý do theo schema                                                                      |
| ----------------- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `drive_038 (1019) | Xe nhỏ ở xa, phần thân mờ, có thể là`car` hoặc `van`.                       | Gán là`car` nếu hình dáng thấp và không có thân van cao; nếu không chắc chắn thì bỏ qua.                        | Chỉ gán khi đủ dữ kiện hình dạng để xác định lớp.                         |
|                   |                                                                                      |                                                                                                                                 |                                                                                         |
| `drive_020(1156)  | Minivan hoặc xe khách nhỏ ở xa, dễ nhầm với`bus` và `car`.                   | Gán là`van` nếu thân cao và dạng xe đa dụng; không gán `bus` nếu không có đặc điểm xe khách tuyến rõ ràng. | Phân biệt theo kích thước và hình dạng; không tự chọn khi chưa chắc chắn. |
| `drive_043        | Vật thể quá nhỏ ở góc ảnh, chỉ còn mảnh không đủ để xác định lớp. | Không gán.                                                                                                                    | Vật thể quá mờ, nhỏ và không chắc chắn nên không đoán.                     |
