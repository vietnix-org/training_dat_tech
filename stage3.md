
# SSL

## SSL là gì?

SSL (Secure Sockets Layer) là một giao thức bảo mật tiêu chuẩn để thiết lập một liên kết được mã hóa giữa máy chủ và trình duyệt. Điều này đảm bảo rằng tất cả dữ liệu được truyền giữa máy chủ và trình duyệt đều riêng tư và an toàn.

## Có bao nhiêu cách chứng thực SSL?

Có ba cách chứng thực SSL chính:

- Chứng thực miền (Domain Validation - DV): Đây là mức độ xác thực cơ bản nhất, chỉ xác minh rằng bạn sở hữu tên miền.
- Chứng thực tổ chức (Organization Validation - OV): Mức độ này xác minh cả quyền sở hữu miền và thông tin của tổ chức.
- Chứng thực mở rộng (Extended Validation - EV): Đây là mức độ cao nhất, yêu cầu xác minh nghiêm ngặt về tổ chức, cung cấp mức độ tin cậy cao nhất cho người dùng.


## CSR file dùng làm gì trong quá trình tạo SSL?

CSR (Certificate Signing Request) là một khối văn bản được mã hóa chứa thông tin công khai về tổ chức của bạn và tên miền mà bạn muốn bảo vệ. Nó được gửi đến nhà cung cấp chứng chỉ SSL (CA) để yêu cầu chứng chỉ SSL.

## Pem file là gì?

PEM (Privacy-Enhanced Mail) là một định dạng chứa chứng chỉ SSL, khóa riêng và đôi khi là cả chuỗi chứng chỉ. Nó thường được sử dụng để lưu trữ và chia sẻ các tệp liên quan đến SSL.

## Private key ssl là gì?

Private key là một tệp chứa một chuỗi ký tự bí mật được sử dụng để giải mã dữ liệu được mã hóa bằng chứng chỉ SSL tương ứng. Nó phải được giữ bí mật và không được chia sẻ với bất kỳ ai.

## PFX file là gì? 

PFX (Personal Information Exchange) là một định dạng chứa chứng chỉ SSL và khóa riêng ở dạng nhị phân. Nó thường được sử dụng để nhập và xuất chứng chỉ SSL trên các máy chủ Windows.

## Cách chuyển từ file crt file sang PFX file

```bash
openssl pkcs12 -export -out domain.pfx -inkey domain.key -in domain.crt
```

# Domain

## Domain là gì?

Domain (tên miền) là một địa chỉ web duy nhất giúp người dùng dễ dàng tìm thấy trang web của bạn trên internet. 

## Các trạng thái của domain

Một số trạng thái phổ biến của domain bao gồm:

- Active: Tên miền hoạt động bình thường.
- Pending: Tên miền đang chờ xử lý đăng ký hoặc gia hạn.
- Expired: Tên miền đã hết hạn và không còn hoạt động.
- Suspended: Tên miền bị tạm ngưng do vi phạm chính sách hoặc không thanh toán.

## Subdomain là gì?

Subdomain là một phần mở rộng của tên miền chính. 

## Virtual Hosts là gì?

Virtual Hosts cho phép chạy nhiều trang web trên cùng một máy chủ bằng cách sử dụng các tên miền hoặc subdomain khác nhau.

# Mail Server

## MX Record

MX (Mail Exchange) record là một loại DNS record chỉ định máy chủ nào chịu trách nhiệm nhận email cho một tên miền cụ thể.

## DKIM, SPF, PTR

-   DKIM (DomainKeys Identified Mail): Một phương pháp xác thực email giúp ngăn chặn giả mạo email.
-   SPF (Sender Policy Framework): Một phương pháp xác thực email khác giúp ngăn chặn giả mạo địa chỉ email người gửi.
-   PTR (Pointer Record): Một loại DNS record ánh xạ một địa chỉ IP đến một tên miền.

## Debug khi khách hàng không nhận được email.

### Một số bước để debug khi khách hàng không nhận được email:

-   Kiểm tra xem email có bị gửi vào thư mục spam hay không.
-   Kiểm tra MX record của tên miền có chính xác không.
-   Kiểm tra log mail server để xem có lỗi gì không.
-   Liên hệ với nhà cung cấp dịch vụ email để được hỗ trợ.

# DNS

## DNS là gì?

DNS (Domain Name System) là một hệ thống phân cấp phân giải tên miền thành địa chỉ IP và ngược lại. Nó giống như một danh bạ điện thoại của internet.

## Các loại recored DNS

Một số loại record DNS phổ biến:

-   A (Address): Ánh xạ một tên miền đến một địa chỉ IPv4.
-   AAAA (IPv6 Address): Ánh xạ một tên miền đến một địa chỉ IPv6.
-   CNAME (Canonical Name): Tạo một bí danh cho một tên miền khác.
-   MX (Mail Exchange): Chỉ định máy chủ mail cho một tên miền.
-   TXT (Text): Lưu trữ thông tin văn bản.

## Nguyên tắc làm việc của DNS

Khi nhập một tên miền vào trình duyệt, trình duyệt sẽ gửi yêu cầu đến DNS resolver để tìm địa chỉ IP tương ứng. DNS resolver sẽ tìm kiếm thông tin trong cache của nó, nếu không tìm thấy, nó sẽ gửi yêu cầu đến các DNS server khác cho đến khi tìm thấy địa chỉ IP.

## Cách phân giải địa chỉ DNS

Có hai cách phân giải địa chỉ DNS chính:

-   Phân giải đệ quy: Trình duyệt gửi yêu cầu đến DNS resolver và DNS resolver chịu trách nhiệm tìm kiếm địa chỉ IP.
-   Phân giải lặp: Trình duyệt gửi yêu cầu đến DNS resolver, DNS resolver trả về địa chỉ của DNS server khác, trình duyệt tiếp tục gửi yêu cầu đến DNS server đó cho đến khi tìm thấy địa chỉ IP.
