# Phiếu QC 1 - Road v1.0

Lô được kiểm (học viên): Đặng Quốc Thái       Người kiểm: rà soát độc lập có AI hỗ trợ
Ngày: 21/11/2026                             Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `annotations.xml` (dangquocthai-front), `annotations.xml` (CVAT, chưa có manifest/revision)
Số ảnh kiểm: 6 ảnh ngẫu nhiên (A05, A06, A08, B01, B02, B06)   Số nhãn đã kiểm: 76 shape + 24 tag = 100 nhãn

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 ảnh | 1 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 ảnh | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 6 ảnh | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 76 shape | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 76 shape | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 76 shape | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 6 ảnh | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 76 shape | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 76 shape | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 76 shape | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 2 ảnh B | 1 | chính |
| QC1-12 file | lỗi file | 2 export | 1 | nhẹ |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | B02_03177_FV.png | camera, tag | nặng | Ảnh fisheye nhưng tag camera có giá trị `front`; cần `fisheye_front`. |
| 2 | QC1-07 | B06_04068_MVL.png | drivable, thiếu | chính | Fisheye-left có mặt đường xe đi được rõ trong export nhưng không có polygon `drivable`. |
| 3 | QC1-11 | B02_03177_FV.png | traffic_light, 4 hộp ngoài vùng | chính | Các hộp đèn ở mép vòng fisheye có `edge_zone=false`; cần kiểm và bật `edge_zone=true` theo ngưỡng 80% bán kính vòng ảnh. |
| 4 | QC1-12 | dangquocthai-front.zip, dangquocthai-fisheye.zip | file, export | nhẹ | Hai export dùng CVAT for images 1.1 hợp lệ nhưng không kèm manifest/revision để xác minh bàn giao theo quy trình. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| B02_03177_FV.png | Xác nhận bán kính vòng fisheye thực tế để đặt `edge_zone` chính xác cho các hộp ở mép. | |
| B06_04068_MVL.png | Xác nhận vùng lái có cần bỏ phần tối viền và thân xe mình trong fisheye-left. | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 2 / 100 nhãn = 2.0%   Lỗi nhẹ: 1   Ca chờ lead: 2
Quyết định (Release / Hold / Rework): Rework
Lý do (theo luật của phiếu): B02_03177_FV.png có tag camera sai, thuộc QC1-01 và là lỗi nặng. Theo luật của phiếu, có ít nhất một lỗi nặng thì kết quả là Rework

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
