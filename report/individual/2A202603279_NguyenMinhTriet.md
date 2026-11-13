# Báo cáo cá nhân — HoVaTen-MSSV

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyễn Minh Triết   
- MSSV: 2A202603279
- Email: trietn0512@gmail.com
- Link repository: https://github.com/Bennguyen05/K5-L2B-DAY4-MinhTrietNguyen-2A202603279-KeypointPose.git
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: hệ điều hành Ubuntu · RAM 16 GB · chạy CVAT chế độ đầy đủ 
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có 
- Giờ bắt đầu: 19h
- Giờ kết thúc: 22h

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` |skeleton|17|Có |Có |20|
| `face` |skeleton|13|Có|Có |13|

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có 

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu): Chuột trái và điểm, chọn outside (nút bên trái) hoặc occluded (thứ 3 từ trái sang).

...

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 1 | 0 | 15 |
| `occluded` | 3 | 5 | 0 | 0 | 8 |
| `back` | 2 | 4 | 0 | 0 | 3 |
| `small` | 1 | 2 | 0 | 0 | 2 |
| `crowd` | 1 | 3 | 0 | 0 | 2 |
| `faces` | 8 |8 | — |0 | 25 |

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1: 30 · CP2: 25 · CP3: 20 
- Ảnh tốn thời gian nhất là ảnh nào, vì sao? Ảnh tốn thời gian nhất là crowd vì tôi phải vẽ skeleton cho nhiều người, và một trong số đó còn có occluded.

...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| 1 | 2 người ngồi trên cùng 1 xe, người trước che gần hết người sau, chỉ để lộ một phần mặt và 2 đầu gối | upper body |outside | không gán hoặc chỉ gán một phần mặt và 2 knee | vẫn có thể xác định rõ đó là một người |
| 2 | người mang kính râm | 2 eyes | outside | đánh dấu là outside hay occluded cho phần mắt | không thể xác định rõ vị trí và kích thước của mắt |
| 3 | người có râu che hết cả miệng | mouth | outside | đánh dấu là outside hay occluded | không thể nhìn rõ phần miệng |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| 000000164659 | #1 | knee, ankle | lr_swap | do người đó để chéo chân nên đánh dấu chéo làm hệ thống cảnh báo | không sửa |
| 000000461002 | #2 | knee, ankle | lr_swap | do người đó xoay người nên hệ thống cảnh báo | không sửa |
| 000000542160 | #3 | hip | lr_swap | do người đó để chân trái lên trước chân phải nên hệ thống cảnh bảo | không sửa |
| 000000580257 | #2 | ankle | lr_swap |do người đó xoay người nên hệ thống cảnh báo | không sửa  |
| 000000580257 | #1 | ankle | lr_swap |do người đó xoay người nên hệ thống cảnh báo | không sửa |
| 178208 | #1 | face | ok  | không có | không sửa |
| 300399 | #1 | face | ok | không có | không sửa |
| 380639 | #1 | face | ok | không có | không sửa |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 5 |0 |0 |0 |0 |3 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn): một số ảnh có thấy một khoảng nhỏ của điểm nhưng không chắc chắn để chọn 'v = 0

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenMinhTriet_persons.zip` | 000000043500.jpg, người #1 | 51 | có: file ghi v=1 ở right_shoulder, left_wrist và v=0 ở nose, left_eye, right_eye, right_elbow, right_wrist | có 12 điểm v > 0 = 10 điểm v=2 + 2 điểm v=1|
| `NguyenMinhTriet_persons.zip` |000000164659.jpg, người #1 | 51 |có: file ghi v=1 ở right_knee, không có điểm v=0 |có (17) |
| `NguyenMinhTriet_faces.zip` |face_53580.jpg |39 |có: file ghi v=0 ở mouth_left, các điểm còn lại v=2 |có (12) |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? Là tọa độ cũ 

Hai job đã chuyển sang completed trên CVAT? Có 

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenMinhTriet_persons.zip
  Số ảnh: 12 · số skeleton `person`: 19 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043500=2, 000000090646=1, 000000100510=2, 000000164659=1, 000000183176=2, 000000241837=1, 000000294329=1, 000000429594=1, 000000445187=1, 000000461002=2, 000000542160=3, 000000580257=2
  Cờ v: v=2 229 (71%) · v=1 39 (12%) · v=0 55 (17%)
  num_keypoints trung bình: 14.1
- File face: NguyenMinhTriet_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_178208=1, face_255797=1, face_300399=1, face_380639=1, face_416730=1, face_490361=1, face_53580=1, face_85624=1
  Cờ v: v=2 95 (91%) · v=1 0 (0%) · v=0 9 (9%)
  num_keypoints trung bình: 11.9
- Ghi chú: 64 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 5
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:
- 000000164659 #1 (knee, ankle): left_knee x=323 < right_knee x=338 và left_ankle x=305 < right_ankle x=355, trong khi các cặp còn lại đúng chiều. Giữ nguyên vì không phải lỗi sai
- 000000461002 #2 (knee, ankle): left_knee x=304 < right_knee x=315 và left_ankle x=304 < right_ankle x=340. Người này nhỏ (khoảng 50×93 px) nên hai chân sát nhau. Giữ nguyên vì không phải lỗi sai
- 000000542160 #3 (hip): hông của người này đúng chiều (left_hip x=326 > right_hip x=291); cặp ngược thực sự là knee (295 < 314) và ankle (303 < 336). Giữ nguyên vì không phải lỗi sai
- 000000580257 #1 (ankle): left_ankle x=458 < right_ankle x=482, trong khi knee và hip đúng chiều. Giữ nguyên vì không phải lỗi sai
- 000000580257 #2 (ankle): left_ankle x=272 < right_ankle x=382. Giữ nguyên vì không phải lỗi sai

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   <img width="479" height="329" alt="image" src="https://github.com/user-attachments/assets/ce09d60e-81d7-48e7-9ff7-7f11c09cd58d" />


2. Một người quay lưng đã gán, cờ đã đặt:

   <img width="281" height="353" alt="image" src="https://github.com/user-attachments/assets/a0877ce9-8103-4a3c-95df-556dd9d97e1d" />


3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   <img width="241" height="283" alt="image" src="https://github.com/user-attachments/assets/093b1e62-af0d-4c66-b388-a1b2cbe87ab0" />


4. Một đoạn JSON xuất của một người:

   {"id":1,"image_id":1,"category_id":1,"bbox":[196.58,132.06,70.54,180.65],"iscrowd":0,
 "keypoints":[248.24,142.15,0,198.64,129.76,0,206.84,130.66,0,199.43,132.06,2,212.25,134.26,2,196.58,152.8,2,221.83,145.83,1,217.36,181.33,2,237.79,174.19,0,205.91,196.42,1,218.16,203.23,0,218.3,197.32,2,240.15,194.54,2,212.91,260.71,2,228.0,252.3,2,220.89,312.71,2,267.12,284.18,2],
 "num_keypoints":12}

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:
Lỗi tôi mắc nhiều nhất là nhầm trái/phải ở chân, nhất là cặp knee và ankle (check_submission.py báo 5 cảnh báo ở 4 ảnh). Nguyên nhân là hai chân nằm sát nhau hoặc chồng lên nhau nên tôi dễ gán điểm của chân này sang bên của chân kia, thay vì luôn tính trái/phải theo cơ thể của chính người đó. Ở dự án thật tôi sẽ:

- Xác định người quay mặt hay quay lưng trước khi chấm.
- Chấm từng chân liền một mạch, từ hông xuống gối rồi cổ chân, để cả chân thuộc về một bên.
- Nếu đường hông, gối, cổ chân của một chân bắt chéo sang chân kia thì dừng lại kiểm tra.
- Chạy checker sớm sau vài ảnh đầu, không chờ đến cuối.

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   Chấm left_* / right_* theo hông trước: sau khi đặt hai hông, knee và ankle của mỗi chân phải nằm cùng phía với hông của chân đó. Nếu hai chân thật sự bắt chéo thì ghi chú "chân bắt chéo" cho ảnh đó, để người review không nhầm với lr_swap. Ảnh ví dụ: 000000164659, người #1 (cặp knee, ankle bị cảnh báo).

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   Tôi chọn lỗi lr_swap ở knee và ankle. Model pose dạng heatmap (như ViTPose) học một kênh heatmap cho mỗi điểm, với mục tiêu là một đỉnh Gaussian đặt đúng tại tọa độ nhãn. Nếu trong một ảnh tôi gán left_knee lên đầu gối phải thật, kênh left_knee bị dạy bật ở đầu gối phải, trong khi các ảnh gán đúng dạy nó bật ở đầu gối trái. Hai nguồn nhãn mâu thuẫn làm heatmap bị nhòe hoặc có hai đỉnh, và trên người quay lưng hoặc chân bắt chéo model sẽ càng dễ đổi trái/phải. Bước lật ảnh cũng không sửa được lỗi này: khi lật ngang, code huấn luyện hoán đổi chỉ số trái/phải của nhãn, nên nhãn sai vẫn sai theo cách tương ứng sau khi lật. Cờ v cũng đi vào loss: theo quy ước COCO điểm v=0 có trọng số 0 (không có tín hiệu học), còn v=1 và v=2 đều được tính, nên chọn nhầm giữa v=1 và v=0 cũng làm model học khác đi.

## 8. Khó khăn và lỗi kỹ thuật

Lỗi git push lên main không được do tôi không điền đúng tên url của repo

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
|1 |3 |0 |Người cúi xuống bị che khuất gần hết |
|2 |2 |2 |Người bị ngựa bò che khuất phần lower body |
|3 |3 |2 |không có |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenMinhTriet_bonus_persons.zip
  Số ảnh: 3 · số skeleton `person`: 8 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000065350=3, 000000161603=2, 000000465508=3
  Cờ v: v=2 83 (61%) · v=1 3 (2%) · v=0 50 (37%)
  num_keypoints trung bình: 10.8
- Ghi chú: 50 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 1
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

- Viền môi và khóe miệng: môi và da gần như cùng độ sáng, nên lip_upper, lip_lower, mouth_left, mouth_right chỉ còn dựa vào bóng đổ và rãnh môi.
- Khóe mắt và mi: lòng trắng, mi và da quanh mắt có độ sáng gần nhau, nên các điểm eye_outer, eye_inner, eye_upper, eye_lower khó đặt chính xác. Tôi phải phóng to và dựa vào hình dạng thay vì màu.
- Với kính râm, cờ v không phụ thuộc vào loại ảnh mà phụ thuộc vào việc điểm đó có nhìn thấy được trong ảnh hay không. Nếu tròng kính vẫn tối và không thấy mắt phía sau thì các điểm mắt vẫn là v = 1 (Occluded), đặt ở vị trí ước lượng. Nếu mắt nhìn thấy rõ xuyên qua kính (một số loại kính râm trong suốt với hồng ngoại gần) thì các điểm mắt là v = 2. Với ảnh nhiệt, kính thường chặn hồng ngoại nhiệt và hiện tối, nên vẫn là v = 1.

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

Dùng claude để hỗ trợ viết báo cáo
