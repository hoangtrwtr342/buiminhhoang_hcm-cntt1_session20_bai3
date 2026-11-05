# Bài 3 : Quản lý rủi ro khi mất thiết bị xác thực


## Báo cáo IPO: Khôi phục quyền truy cập AWS
- Input (Đầu vào)

    IAM Username và Password hiện tại.
    
    01 Backup Code hợp lệ (được lưu trữ ngoại tuyến từ trước).
    
    Thiết bị thay thế mới (máy tính an toàn, điện thoại mới hoặc khóa phần cứng FIDO2/YubiKey).

- Process (Quy trình xử lý)

    Xác thực khẩn cấp: Đăng nhập AWS Console, chọn tính năng khắc phục sự cố MFA (Troubleshoot MFA) và nhập Backup Code thay thế mã 6 số.
    
    Hủy phiên đăng nhập: Vào IAM > Security credentials, chọn Revoke active sessions để buộc đăng xuất mọi phiên làm việc đang duy trì trên điện thoại thất lạc.
    
    Hủy thiết bị cũ: Chọn Deactivate thiết bị MFA gắn với Google Authenticator của máy cũ để vô hiệu hóa ngay lập tức các mã OTP sinh ra từ máy đó.
    
    Đổi mật khẩu: Cập nhật mật khẩu IAM mới đề phòng mật khẩu cũ bị lưu trên trình duyệt máy đã mất.
    
    Cấp mới MFA & Mã dự phòng: Đăng ký thiết bị MFA mới, đồng bộ TOTP và tải về bộ Backup Codes mới (hủy bỏ hoàn toàn bộ mã cũ).
    
    Kiểm tra nhật ký: Rà soát AWS CloudTrail từ thời điểm mất điện thoại để đảm bảo không có truy cập trái phép.

- Output (Đầu ra)
    
    Khôi phục thành công quyền truy cập để bảo trì hệ thống.
    
    Vô hiệu hóa triệt để khả năng truy cập từ điện thoại đã mất.
    
    Tài khoản được bảo vệ an toàn bởi lớp MFA và bộ Backup Codes mới.

## Lý do không lưu Backup Codes dạng ảnh trong thư viện điện thoại
  - Tự phá vỡ nguyên tắc MFA (Single Point of Failure): MFA bảo vệ tài khoản bằng việc tách biệt "thứ bạn biết" (mật khẩu) và "thứ bạn sở hữu" (thiết bị/mã dự phòng). Nếu lưu cả ứng dụng Authenticator lẫn ảnh Backup Code trên cùng một máy, kẻ nhặt điện thoại chỉ cần mở được khóa màn hình là có toàn quyền đăng nhập.
  
  - Nguy cơ rò rỉ qua đồng bộ đám mây: Thư viện ảnh thường tự động đồng bộ lên Google Photos, iCloud hoặc OneDrive. Khi tài khoản cá nhân này bị rò rỉ, Backup Code sẽ bị lộ từ xa dù không ai chạm vào máy vật lý.
  
  - Quyền truy cập của ứng dụng bên thứ ba: Nhiều ứng dụng trên điện thoại yêu cầu quyền truy cập toàn bộ thư viện ảnh, dễ tạo cơ hội cho mã độc quét và đọc dữ liệu nhạy cảm.
