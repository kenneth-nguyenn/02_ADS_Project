# 02_ADS_Project
Đồ án Khoa học Dữ liệu Ứng dụng

## Thông tin giảng viên: 
- Trần Trung Kiên
- Nguyễn Thái Vũ

## Thông tin nhóm 02:
1. Thành viên:

| STT | MSSV | Họ tên | Github |
| --- | --- | --- | --- |
| 1 | 1712727 | Nguyễn Hoàng Sơn | [hsjune29th](https://github.com/hsjune29th) |
| 2 | 1712258 | Nguyễn Văn Hậu | [kenneth-nguyenn](https://github.com/kenneth-nguyenn) |
| 3 | 1712888 | Nguyễn Đình Tuyên | [Tuyen177](https://github.com/Tuyen177) |

2. Phân công công việc: [Google Sheet](https://docs.google.com/spreadsheets/d/1eKbhc6rpNsDoBfTC8SfAnlKiw_y3_OvHUefUuxQw8BI/edit#gid=621371829)

## Mô tả bài toán:
- **Tên cuộc thi:** [Google Brain - Ventilator Pressure Prediction](https://www.kaggle.com/competitions/ventilator-pressure-prediction/data?select=test.csv)
- **Mô tả:** Được tổ chức bởi Google Brain vào 04/11/2021 với hơn 2,605 nhóm tham dự.
- **Input:** Tập dữ liệu được thu thập từ máy thở cung cấp khí oxy cho phổi.
- **Output:** Dự đoán áp lực trên đường thở (pressure).
- **Bài toán: Regression**
- **Ý nghĩa thực tiễn của ứng dụng:**
    + Trên thực tế, trong thở máy có 3 mode thở cơ bản là: Kiểm soát, Hỗ trợ, Tự thở.
        + Ứng với Kiểm soát (control/limit), có 3 loại kiểm soát:
            + Pressure Controlled: Giới hạn áp lực, cài đặt Pi, thể tích thay đổi.
            + Volume Controlled: Mục tiêu thể tích, cài đặt Vt, áp lực thay đổi.
            + Dual Controlled: Mục tiêu thể tích và giới hạn áp lực, cài đặt Vt, máy tự điều chỉnh Pi.
        + Công việc của các bác sĩ lâm sàng là theo dõi bệnh nhân thở máy về: Áp lực đường thở và Thể tích khí lưu thông.
        + Ưu điểm của Pressure Control:
            + Hạn chế báo động áp lực cao.
            + Cải thiện sự phân phối khí trong phổi.
            + Và một số ưu điểm khác liên quan đến các con số trong y khoa.
        + Khuyết điểm của Pressure Control: Vt thay đổi khi phổi thay đổi R và C:
            + Vt quá lớn thì quá căng phế nang.
            + Vt quá nhỏ thì giảm thông khí phế nang, ứ CO2.
        + Ứng dụng lâm sàng:
            + Dùng cho trẻ sơ sinh dưới (10kg).
            + Bệnh nhân có tổn thương phổi (R cao hoặc C thấp).
            + Nhiều nghiên cứu so sánh Pressure và Volume Control chỉ ra Pressure cải thiện oxy trong máu tốt hơn, ít biến chứng, phù hợp nhu cầu của bệnh nhân.
    + Thở máy là một biện pháp chuyên sâu của bác sĩ lâm sàng. Dưới sự khẩn thiết của đại dịch COVID-19 trên diện rộng, ta dễ dàng thấy hạn chế của việc sử dụng phương pháp thở máy này. Việc phát triển các phương pháp mới để điều khiển máy thở cơ học rất tốn kém, gặp khó khăn khi thử nghiệm lâm sàng.
    + Nhóm nghiên cứu tại Google Brain tin rằng, khi đã có thông tin R và C của phổi bệnh nhân, cùng với sự kiểm soát lượng khí đi vào phổi, ta hoàn toàn có thể điều khiển Pi một cách tự động, thích nghi nhanh chóng.
Bài toán này cũng là tiền đề cho các thuật toán thích ứng với bệnh nhân, giúp giảm bớt gánh nặng cho bác sĩ lâm sàng trong tình hình mới. Do đó, các phương pháp điều trị bằng máy thở có thể được phổ biến rộng rãi hơn để giúp bệnh nhân thở dễ dàng.

## Giải quyết bài toán:
1. Phần 1 - Training model DNN trên Kaggle: File "Report.jpynb" chứa nội dung mang tính trình bày báo cáo, phần train được tập trung trong [Notebook build Model](https://www.kaggle.com/code/kennethnguyen/step-01-build-7-bidirect-lstm-model).
2. Phần 2 - Ensembling: Sử dụng hàm `better_than_median()` được đề cập ở mục "3.5. Tập hợp các dự đoán pressure của bảy model" trong "Report.jpynb".
3. Phần 3 - PID Controller: Được trình bày từ mục "3.6. The Inverse PID Controller" trong "Report.jpynb".

## Kết quả submission trên Kaggle:
1. Score trên Private Leaderboard: **0.2364**.
2. Rank trên Private Leaderboard: 1632/2605.

## Hướng phát triển:
- Tuning parameters quá trình training model và điều chỉnh PID để đạt thứ hạng cao hơn, kết quả tốt hơn.
