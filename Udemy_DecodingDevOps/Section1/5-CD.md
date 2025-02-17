# Tóm tắt về Continuous Delivery (CD) trong DevOps

## 1. Giới thiệu về Continuous Delivery (CD)

- **Continuous Delivery (CD) là quy trình tự động triển khai code lên máy chủ nhanh chóng và hiệu quả.**
- CD là **mở rộng của Continuous Integration (CI)**.
- **Mục tiêu**: **Tự động hóa** mọi bước trong quá trình triển khai để giảm lỗi và tăng tốc độ phát hành phần mềm.

## 2. Mối quan hệ giữa CI và CD

- CI tự động **xây dựng (build) và kiểm thử (test)** code → tạo ra artifact (phần mềm).
- Ops team nhận yêu cầu triển khai artifact lên server.
- **Vấn đề**:
  - **Triển khai thủ công** dễ gặp lỗi, mất nhiều thời gian.
  - **Nhiều bước phức tạp**:
    - Cấu hình server, cài đặt dependencies, thay đổi mạng/firewall, triển khai artifact.
  - **Quá nhiều can thiệp của con người** dẫn đến **lỗi và chậm trễ**.

## 3. Giải pháp Continuous Delivery (CD)

- **Tự động hóa toàn bộ quy trình triển khai**:
  - **Server provisioning**: Chuẩn bị hạ tầng.
  - **Cài đặt dependencies**: Đảm bảo môi trường đúng phiên bản.
  - **Triển khai artifact**: Đưa phần mềm lên server.
  - **Kiểm thử tự động**: Chạy các bài kiểm thử chức năng, hiệu suất, bảo mật.
- **Kết hợp CI/CD** → **Tích hợp Dev, Ops, QA thành một quy trình thống nhất**.

## 4. Các công cụ hỗ trợ Continuous Delivery

- **Tự động hóa hệ thống**: Ansible, Puppet, Chef.
- **Tự động hóa hạ tầng cloud**: Terraform, CloudFormation.
- **CICD Pipeline**: Jenkins, Octopus Deploy.
- **Kiểm thử tự động**: Selenium, JMeter, SonarQube.

## 5. Lợi ích của Continuous Delivery

- **Giảm thiểu lỗi triển khai** nhờ tự động hóa.
- **Tăng tốc độ phát hành phần mềm**, giảm lead time.
