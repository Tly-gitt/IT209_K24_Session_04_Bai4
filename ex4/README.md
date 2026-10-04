# Báo Cáo:
## 1. Giải thích lệnh `git rm --cached`
- **Mục đích:** Gỡ bỏ tệp khỏi vùng theo dõi của Git (Staging Area/Index) mà vẫn giữ lại tệp vật lý trên đĩa cứng (Working Directory).
- **Cơ chế hoạt động:** 
  - Khác với `git rm` thông thường (vừa xóa cache vừa xóa file trên ổ đĩa), tùy chọn `--cached` chỉ tác động đến cơ sở dữ liệu theo dõi của Git. 
  - Sau khi chạy lệnh, Git coi tệp là một tệp mới chưa được theo dõi (Untracked). Khi kết hợp cấu hình tên tệp vào `.gitignore`, Git sẽ tự động lờ đi tệp này trong tương lai, tránh rò rỉ dữ liệu nhạy cảm.

## 2. Các bước đã thực hiện
1. **Gỡ tệp nhạy cảm khỏi cache:**
   ```bash
   git rm --cached credentials.txt
   ```
2. **Cấu hình .gitignore:**
   ```bash
   echo "credentials.txt" >> .gitignore
   git add .gitignore
   ```
3. **Cập nhật commit gần nhất bằng --amend:**
   ```bash
   git commit --amend -m "feat: Initialize application logic and ignore credentials"
   ```

## 3. Minh chứng kết quả kiểm tra

### Kết quả `git status`:
```text
On branch main
nothing to commit, working tree clean
```

### Kết quả `git log -n 1 --stat`:
```text
commit daadebc0cda74c4a649aa1c8116c8b0ee40e514f (HEAD -> main)
Author: dangToan <dangtoan.2k6@gmail.com>
Date:   Sun Oct 4 19:08:20 2026 +0700

    feat: Initialize application logic and ignore credentials

 .gitignore | 1 +
 index.js   | 1 +
 2 files changed, 2 insertions(+)
\`\`\`
*(credentials.txt đã được loại bỏ hoàn toàn khỏi lịch sử commit)*