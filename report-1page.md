# FIT4012 Lab 7 - Báo cáo 1 trang: SHA-256

## 1. Mục tiêu / Objective

Mô tả ngắn gọn mục tiêu của bài thực hành: phân tích thuật toán SHA-256, chạy chương trình băm chuỗi, kiểm tra toàn vẹn file, băm mật khẩu và cải tiến bằng salt.

## 2. Cách làm / Approach

Tóm tắt cách nhóm/cá nhân đã thực hiện:

- Biên dịch và chạy `sha_procedure.cpp`.
- Kiểm thử SHA-256 bằng known answer test vector.
- Viết/chạy chương trình kiểm tra toàn vẹn file.
- Viết/chạy chương trình băm mật khẩu.
- Bổ sung salt để tránh việc hai người có cùng mật khẩu tạo ra cùng hash.

## 3. Kết quả / Result

- Hash của chuỗi `abc`:
  → ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad

- Hash của file mẫu trước khi sửa:
  → (chạy: printf "FIT4012 SHA sample\n" > sample.txt && ./sha256 --hash-file sample.txt)

- Kết quả kiểm tra file sau khi sửa nội dung:
  → [FAIL] File was changed or expected hash is incorrect

- Kết quả đăng nhập với mật khẩu đúng:
  → [PASS] Login success

- Kết quả đăng nhập với mật khẩu sai:
  → [FAIL] Login failed: wrong password

- Hai bản ghi salt:hash của cùng một mật khẩu có giống nhau không?
  → Không, vì salt ngẫu nhiên khác nhau mỗi lần đăng ký.

## 4. Kết luận / Conclusion

- SHA-256 phát hiện thay đổi vì chỉ cần 1 byte thay đổi là toàn bộ hash thay đổi hoàn toàn (avalanche effect).
- Cần salt để tránh hai người cùng mật khẩu sinh ra cùng hash, ngăn tấn công rainbow table.
- SHA-256 không phù hợp xác thực thật vì quá nhanh — attacker có thể brute-force hàng tỷ lần/giây; cần Argon2id/bcrypt/scrypt vì các thuật toán này được thiết kế để chậm và tốn RAM.
