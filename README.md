![image](https://github.com/user-attachments/assets/90a3ef03-2346-4245-ad1b-c3efee2de494)# Traffic-Sign-Detection
## Link Datasets: https://s.net.vn/FDDB
&nbsp;&nbsp;&nbsp;Dataset gồm 2 filder là images và annotations:

  ![image](https://github.com/user-attachments/assets/b1060bd9-8f11-4e55-887b-8e091ff1d088)

&nbsp;&nbsp;&nbsp;annotations gồm các file .xml có chứa thông tin của ảnh như tên file, width, height, label, bounding box, ...

## 1. Tiền xử lý ảnh đầu vào và huấn luyện mô hình:
<p> &nbsp;&nbsp;&nbsp;Sử dụng thuật toán HoG để chuyển ảnh ban đầu thành vector đơn giản hơn mà vẫn giữ được các đặc trưng </p>
&nbsp;&nbsp;&nbsp;Sau đó đưa dữ liệu vào mô hình SVM để huấn luyện mô hình

## 2. Xác định vị trí vật thể trong ảnh:
&nbsp;&nbsp;&nbsp; Sử dụng Sliding Window có kích thước cố định để trượt qua toàn bộ bức ảnh

![image](https://github.com/user-attachments/assets/69fa1bfd-63c1-4969-9d1b-f72d6e24cb1d)

&nbsp;&nbsp;&nbsp;Đối với vật thể có kích thước quá nhỏ so với sliding window thì sử dụng phương pháp Pyramid Image. Ta scale thu nhỏ dần tấm hình gốc lại để object bé được phóng lớn hơn -> window sẽ vừa và dễ dàng tìm thấy object hơn.

![image](https://github.com/user-attachments/assets/7c7d9b3d-0ed6-4ab0-bfe3-f857bc4570ec)

## 3. Dự đoán:
&nbsp;&nbsp;&nbsp; Sử dụng mô hình SVM đã huấn luyện để dự đoán, kết quả là các bounding box bị chồng lên nhau. Để giải quyết vấn đề này thì áp dụng Non-maximum suppression. Đầu tiền, aắp xếp các bounding box giảm dần theo giá trị confidence score.Tính IoU giữa giá trị bounding box có confidence score lớn nhất với tất cả những cái còn lại và chỉ giữ lại những bounding box có IoU nhỏ hơn một ngưỡng nào đó
