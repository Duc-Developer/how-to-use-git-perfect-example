Những branch chính
Có 2 branch chính: develop và master
-	Khi source code bên develop đạt đến một mức độ ổn định nào đó và sẵn sàng để release thì sẽ được merge sang bên master và đánh dấu với release number.
-	Khi có thay đổi được merge vào master thì tức là sẽ có một phiên bản production mới được release. Nhờ đó chúng ta có thể sử dụng script để tự động build lên production server mỗi khi có commit ở master.
Những branch phụ
Feature branches
-	Tách từ: develop
-	Merge vào: develop
-	Naming convention: feature-<Tên feature>-*
-	Commit message: <Tên feature>-<Nội dung thay đổi>
Feature branches sử dụng để phát triển feature mới, chức năng mà chưa rõ thời điểm chức năng tích hợp vào hệ thống. Nó sẽ được merge lại vào develop khi quyết định release bao gồm chức năng đó hoặc bỏ đi khi không còn cần thiết.
Tạo feature branch:
$ git checkout -b myfeature develop
Merge vào develop
$ git checkout develop
$ git merge --no-ff myfeature
$ git branch -d myfeature
$ git push origin develop
Release branches
-	Tách từ: develop
-	Merge vào: develop và master
-	Naming convention: release-* 
-	Commit message: <Tên phiên bản> <Số hiệu phiên bản>
Release branches được sử dụng để chuẩn bị cho release mới. Tất cả các công việc cuối cùng trước khi release sẽ được thực hiện ở đây, như fix nốt các bugs lẻ tẻ, chuẩn bị meta-data (version number, build dates, etc..). Không bổ sung feature mới lên branch này.
Tạo release branches
$ git checkout -b release-1.2 develop
$ ./Acm-version.sh 1.2
$ git commit -a -m "Acm 1.2"
Kết thúc release branch, merge vào master và develop và xoá branch
$ git checkout master
$ git merge --no-ff release-1.2
$ git tag -a 1.2
$ git checkout develop
$ git merge --no-ff release-1.2

$ git branch -d release-1.2
Hotfix branches
-	Tách từ: master
-	Merge vào: develop và master
-	Naming convention: hotfix-* 
-	Commit message: <Tên phiên bản> <Số hiệu phiên bản> <Nội dung hotfix>
Hotfix branches được sử dụng khi có một bug nghiêm trọng trên bản master cần giải quyết ngay lập tức, một hotfix-branch sẽ được tách ra từ master và đánh version để nhận biết.
Tạo hotfix branch
$ git checkout -b hotfix-1.2.1 master
$ ./acm-version.sh 1.2.1
$ git commit -a -m "Acm 1.2.1"
(Sau khi hoàn thành)
$ git commit -m " Acm 1.2.1 Fixed severe production problem"
Kết thúc hotfix branch, merge vào master và develop và xoá branch
$ git checkout master
$ git merge --no-ff hotfix-1.2.1
$ git tag -a 1.2.1

$ git checkout develop
$ git merge --no-ff hotfix-1.2.1

$ git branch -d hotfix-1.2.1
