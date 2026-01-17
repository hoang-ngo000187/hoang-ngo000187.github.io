---
layout: post
title: PHẦN 01. GIỚI THIỆU VỀ RTOS
categories: [rtos]
---
# 1. Real Time Application (RTA) là gì?
## 1.1 Tưởng tượng và thực tế
**Tưởng tượng**: Tính toán Real – time (The Real – Time Computing) tương đương với tính toán nhanh (fast computing)

**Thực tế**: Tính toán Real – time tương đương với tính toán có thể dự đoán trước (Predictable Computing)

Từ “Real – Time” thường được sử dụng trong bối cảnh Real Time Application hoặc Real Time operating system.

*“Real time deals with guarantees, not with raw speed.”*

Bất kỳ khi nào ta nói một thứ gì đó là Real Time, tính đúng lúc (timeliness) rất là quan trọng. Nó hứa hẹn sẽ đáp ứng thời hạn của nó cho một thời gian nhất định thay vì chỉ nói về tốc độ thô.

Vì thế, những nhà phát triển ứng dụng (Application Developer) nghĩ rằng họ cần một hệ thống real time cho hiệu suất tốt hơn ứng dụng của họ, họ đòi hỏi đơn giản là nâng cấp phần cứng (hardware) với bộ xử lý (processor) nhanh hơn, nhiều RAM hơn, đường bus tốc độ cao, … Tuy nhiên, điều này không làm cho một hệ thống trở nên “real time”.

Nếu một ứng dụng với phần cứng giới hạn, nếu nó có thể đáp ứng việc chấp hành tính đúng lúc (timeliness excution), khi đó ứng dụng hoặc hệ thống đó có thể gọi là Real time.

## 1.2 Real time là gì?
Một hệ thống Real time là một hệ thống trong đó tính đúng đắn của tính toán không chỉ phụ thuộc vào tính đúng đắn logic của tính toán mà còn phụ thuộc vào thời gian tại thời điểm mà kết quả được tạo ra. Nếu các ràng buộc thời gian không được đáp ứng, lỗi hệ thống được cho là xảy ra.

Ví dụ:
![alt text](/assets/posts/phan1_rtos/image.png) 

Đường màu đỏ cho thấy Non – Real Time Application và đường màu tím biểu thị Real Time Application. Đồ thị Response time (thời gian đáp ứng) theo Execution Interations (tương tác thực thi).

Có thể thấy trong suốt nhiều tương tác thực thi, thời gian đáp ứng của RTA hầu như là hằng số vào khoảng 2,5s cho mỗi tương tác. Với NRTA, thời gian đáp ứng thay đổi rất nhiều. Với tương tác đầu tiên, từ 4s đến tương tác thứ 2 khoảng 1,5s, và tương tác tiếp theo vào khoảng 2,5s.

⮕ Non – Real Time Application không đáp ứng việc chấp hành tính đúng lúc.

## 1.3 Real Time Application là gì?
RTAs không phải là ứng dụng thực thi nhanh, nó không cần nhanh mà phải đáp ứng phản hồi thời gian nghiêm ngặt nhất định. 

RTAs là ứng dụng mang tính xác định về thời gian, điều này có nghĩa là thời gian đáp ứng của nó đối với các sự kiện hầu như là hằng số.

Có thể có độ chênh lệch nhỏ trong thời gian đáp ứng RTAs, trong điều khoảng của ms hoặc giây cái mà sẽ rơi vào thể loại soft real time application.

Hard real time functions phải hoàn thành trong một thời gian nhất định giới hạn, không làm như vậy sẽ dẫn đến thất bại tuyệt đối của hệ thống.
![alt text](/assets/posts/phan1_rtos/image-1.png)

# 2. What is Real Time Operating System (RTOS)?
## 2.1 Real – Time Application
*“Time Deterministic – Response time to events is always almost constant.”*

Chạy Real – Time Application như thế nào?

Bạn không thể tạo một Real – Time Application và chạy nó trên General Purpose Operating System (GPOS) như là Window hoặc Linux, bởi vì nó không bao giờ giúp ta đáp ứng yêu cầu nghiêm ngặt về thời gian.

Thứ ta cần là một hệ điều hành thời gian thực (Real time operating system), cái mà được tùy chỉnh để đạt được những yêu cầu về tính xác định thời gian.

## 2.2 What is a Real Time OS?
Nó là một hệ điều hành (OS), được thiết kế đặc biệt để chạy những ứng dụng (applications) với độ chính xác cao về thời gian và mức độ tin cậy cao.

Để được coi là “real – time”, một hệ điều hành phải có một thời gian tối đa cho mỗi hoạt động quan trọng mà nó thực hiện. Một số các hoạt động này bao gồm:
+ Handling of interrupts and internal system exceptions (xử lý ngắt và những hệ thống nội bộ ngoại lệ).
	Không giống như các hệ điều hành GPOS khác, trong hệ điều hành thời gian thực (RTOS), độ trễ ngắt được giữ ở mức tối thiểu nhất có thể.
+ Handing of Critical Sections. (xử lý mã phần quan trọng).
	Trong hệ điều hành thời gian thực, bạn không tìm thấy các đoạn mã phần quan trọng khổng lồ nơi các ngắt của hệ thống bị tắt.
+ Scheduling Mechanism, v.v…
	Không giống như General Purpose OS, cơ chế lập lịch (Scheduling Mechanism) trong RTOS rất đơn giản và hầu hết thời gian đều ủng hộ tác vụ có mức độ ưu tiên cao.
![alt text](/assets/posts/phan1_rtos/image-2.png)
*The VxWORKS is basically from the company called Windriver, which is acquired by Intel around maybe 10 years ago, and it is widely used in the field of safety, security, IOT, etc..  The VxWORKS is a proprietary software, and you need to have a license to use that in your application.*

*Next one is QNX Neutrino by company called QNX.  This Real-time operating system is majorly used in industrial automation applications, medical and also in robotics.*

*The next one is FreeRTOS. The FreeRTOS is from freertos.org.  This is also one of the famous Realtime operating system among developers.  FreeRTOS comes with two flavours actually.  One is called Open RTOS and another one is Safe.*

*The next one is Integrity.  This is from Green Hills software majorly used for security and safety related applications.*

Nói một cách chính xác, các hệ điều hành di động như Android và iOS có thể không thuộc loại hệ điều hành dành cho mục đích chung (GPOS) thuần túy. Bạn có thể xem xét chúng trong danh mục Hệ điều hành nhúng (Embedded Real – Time OS). 

Tất cả hệ điều hành thời gian thực vừa thảo luận sẽ thuộc loại Hệ điều hành thời gian thực nhúng. (Embedded Real – Time Operating System).

# 3. RTOS vs GPOS: Task Scheduling
# 3.1 GPOS Task Scheduling
GPOS được lập trình để xử lý việc scheduling theo cách mà nó quản lý để đạt được throughput cao.
Throughput có nghĩa là tổng số quá trình (processes) hoàn thành việc thực thi (execution) của chúng trên một đơn vị thời gian (unit time).

Trong những trường hợp như vậy, đôi khi việc thực hiện quá trình có mức độ ưu tiên cao (high priority process) sẽ bị trì hoãn để phục vụ 5 hoặc 6 tác vụ có mức độ ưu tiên thấp (low priority task). High throughput đạt được bằng cách phục vụ 5 tác vụ có mức độ ưu tiên thấp hơn so với việc phục vụ 1 tác vụ có mức độ ưu tiên cao duy nhất.

Vì thế, nếu 5 hoặc 6 tasks có mức độ ưu tiên thấp hơn đang đợi để thực thi, thì GPOS có thể trì hoãn 1 hoặc 2 task có mức độ ưu tiên cao hơn nhằm để tăng throughput.

Trong GPOS, scheduling thường sử dụng chính sách công bằng (fairness policy) để gửi các thread và các process lên CPU.

Chính sách như vậy cho phép throughput tổng thể cao được yêu cầu bởi các ứng dụng máy tính và máy chủ, nhưng không đảm bảo rằng các thread hoặc process có mức độ ưu tiên cao, quan trọng về thời gian sẽ thực thi theo các thread có mức độ ưu tiên thấp hơn.
# 3.2 RTOS – Task scheduling
Mặc khác ở RTOS, các thread thực thi theo thứ tự ưu tiên của chúng. Nếu một thread ưu tiên cao sẵn sàng chạy, nó sẽ tiếp quản CPU từ bất kỳ thread nào có độ ưu tiên thấp hơn mà có thể đang thực thi.

Ở đây, một thread có mức độ ưu tiên cao sẽ được thực thi so với các thread có mức độ ưu tiên thấp. Tất cả “việc thực thi thread có mức độ ưu tiên thấp” sẽ bị tạm dừng. Việc thực thi thread có mức độ ưu tiên cao sẽ chỉ bị ghi đè nếu một yêu cầu đến từ một thread thậm chí là thread ưu tiên cao.

Điều này có nghĩa, RTOS có throughput rất tệ hay không?

Sự thật là Hệ điều hành thời gian thực (RTOS) có thể mang lại throughput ít hơn Hệ điều hành mục đích chung (GPOS) vì nó luôn ưu tiên nhiệm vụ ưu tiên cao để thực thi trước, nhưng điều đó không có nghĩa là, nó có throughput rất kém. Bởi vì những hệ điều hành như GPOS, RTOS được sử dụng hoàn toàn ở những ngữ cảnh khác nhau. GPOS luôn được tải với các process nặng và nhiều process hơn. Nhưng hệ điều hành thời gian thực (RTOS) hầu hết thời gian được tải với số lượng task ít hơn. Vì vậy throughput thực sự có liên quan đến tải trọng của hệ thống. 

Một hệ điều hành RTOS chất lượng vẫn sẽ cung cấp một throughputs tổng thể khá tốt nhưng có thể hy sinh thông lượng để mang tính xác định hoặc để đạt được khả năng dự đoán thời gian.
![alt text](/assets/posts/phan1_rtos/image-3.png)
 
Đối với RTOS, việc đạt được khả năng dự đoán (achieving predictability) hoặc bản chất xác định thời gian (time deterministic nature) quan trọng hơn thông lượng, nhưng đối với GPOS, việc đạt được thông lượng cao hơn để thuận tiện cho người dùng là quan trọng hơn.

# 4. RTOS vs GPOS: Latency
Trong tin học, Latency có nghĩa “Thời gian trôi qua giữa một kích thích (stimulus) và phản ứng với nó".

Task switching latency (độ trễ chuyển đổi tác vụ) có nghĩa là, khoảng cách thời gian đó giữa “Việc kích hoạt một sự kiện và thời gian mà tác vụ xử lý sự kiện đó được phép chạy trên CPU”.

Ví dụ với trường hợp sau:
![alt text](/assets/posts/phan1_rtos/image-4.png)
+ Ở thời điểm t_1, một sự kiện được kích hoạt hoặc xảy ra (ví dụ: phát hiện tai nạn)
+ Tại thời điểm t_2, task (nhiệm vụ) mà xử lý phát hiện tai nạn như Airbag deployment task (nhiệm vụ triển khai túi khí) được thực hiện để chạy trên CPU.
+ Khoảng thời gian từ t_1 đến t_2 được gọi là Task switching latency.
![alt text](/assets/posts/phan1_rtos/image-5.png)
+ Trong trường hợp RTOS, khoảng thời gian này luôn được tinh chỉnh và bị giới hạn. Hệ điều hành thời gian thực luôn giúp bạn thiết kế những loại hệ thống nơi mà khoảng thời gian này phải có tính xác định hoặc giới hạn thời gian. Bất kể khi nào sự kiện diễn ra, khoảng thời gian này luôn gần như không đổi.
+ Nhưng điều trên thì không xảy ra với hệ điều hành mục đích chung (GPOS) nơi mà khoảng thời gian trên thay đổi theo thời gian trôi qua hoặc tải hệ thống tăng lên.
![alt text](/assets/posts/phan1_rtos/image-6.png)

Nhìn vào đồ thị trên, ta thấy khi số lượng tasks Scheduled (system load) tăng lên, Task switching latency cho một task tăng lên trong trường hợp GPOS, nhưng trong trường hợp RTOS, nó luôn hầu như là hằng số.

**RTOS vs GPOS: Interrupt Latency**
![alt text](/assets/posts/phan1_rtos/image-7.png)

Interrupt Latency là khoảng cách thời gian giữa thời điểm mà kích hoạt ngắt (interrupt triggers) và thời điểm mà ISR được bắt đầu thực thi trên CPU.

Task 1 được chạy trên CPU và ở thời điểm t_1 ngắt xảy ra. Nếu nó là một mức độ ưu tiên cao hơn, thì nó sẽ bắt đầu tác vụ này và ISR sẽ bắt đầu thực thi.

Do đó khoảng cách thời gian giữa t_1 và t_2 được gọi là interrupt latency. Interrupt latency này là một thông số rất quan trọng để phục vụ những sự kiện quan trọng. Ví dụ: trong ứng dụng Airbag deployment, khoảng cách này phải nằm trong khoảng us hoặc ns.

Interrupt Latency là một nét đặc trưng quan trọng của RTOS và RTOS nên có khoảng thời gian Interrupt latency này càng nhỏ càng tốt. Và GPOS khoảng cách thời gian này thay đổi khi tải hệ thống tăng lên và nó không bị giới hạn.

Khi ISR kết thúc, bây giờ nó phải chuyển sang tác vụ ưu tiên cao hơn đã sẵn sàng trong hệ thống, phải không?

Vì vậy, khi nó kết thúc ở thời điểm t_3, một trong hai task cũ có thể tiếp tục nhưng đã bị gián đoạn do ISR. Chỉ khi nó là task sẵn sàng có mức ưu tiên cao nhất. Hoặc nó có thể chuyển sang một số task khác được ưu tiên cao hơn vào lúc này.
Khoảng cách thời gian giữa thời điểm ISR hoặc task rời khỏi CPU và thời điểm task mới chuyển vào CPU được gọi là Scheduling latency.

Trong khoảng thời gian này các hoạt động khác nhau diễn ra như lưu ngữ cảnh của một nhiệm vụ cũ (saving the context of an old task) và truy xuất bối cảnh của nhiệm vụ mới (retrieving that context of the new task), mà chúng tôi gọi là chuyển đổi ngữ cảnh (context switching).

Và đối với một ứng dụng thời gian thực, Scheduling latency này phải rất hẹp. Vì vậy, khoảng cách thời gian này phải rất nhỏ càng tốt và đó là một trong những đặc điểm của hệ điều hành thời gian thực.

**Kết luận**: cả Scheduling latency và Interrupt latency của hệ điều hành thời gian thực (RTOS) thì nhỏ nhất có thể bị giới hạn và nó sẽ không tăng khi tải hệ thống tăng. Nhưng trong GPOS, nó không bị giới hạn và độ trễ có thể thay đổi khi tải hệ thống tăng lên.

# 5. RTOS vs GPOS: Priority inversion (đảo ngược ưu tiên)
Giả sử bạn đang đi ra đường với chiếc ô tô màu đen và ô tô của bạn là phương tiện có mức độ ưu tiên thấp.
![alt text](/assets/posts/phan1_rtos/image-8.png)

Xe bạn đang đi vào một ngã tư, và có một số ô tô khác (ô tô màu xanh) đang dừng lại do một sự cố nào đó và xe của bạn bị kẹt lại ở giữa ngã tư.
![alt text](/assets/posts/phan1_rtos/image-9.png)

Bỗng nhiên bạn nghe thấy tiếng còi xe cấp cứu đang đi đến bệnh viện cần băng ngang qua ngã tư. Xe cấp cứu là phương tiện có mức độ ưu tiên cao. Bây giờ, xe cấp cứu không thể băng qua ngã tư vì xe của bạn đang bị kẹt ở giữa ngã tư.
![alt text](/assets/posts/phan1_rtos/image-10.png)

Vì thế, xe cấp cứu bây giờ phải đợi cho tới khi bạn di chuyển được ra khỏi giữa ngã tư thì nó mới di chuyển được. 

Điều này có nghĩa rằng, một phương tiện có mức độ ưu tiên cao hơn đang đợi một phương tiện có độ ưu tiên thấp hơn để di chuyển.

Đó chính xác là Priority Inversion (sự đảo ngược mức độ ưu tiên) là phương tiện có mức độ ưu tiên cao hơn hoạt động giống như xe có mức độ ưu tiên thấp hơn và xe có mức độ ưu tiên thấp hơn sẽ hoạt động giống như xe có mức độ ưu tiên cao hơn.

Đây là trường hợp minh họa cho Priority Inversion. Bây giờ hãy ứng dụng điều này vào ngôn ngữ tin học:
+ Ô tô của bạn (màu đen) là một task có mức độ ưu tiên thấp (low priority task), và những chiếc xe Taxi (màu xanh) là những task có mức độ ưu tiên trung bình (medium priority tasks) và xe cấp cứu là một task có mức độ ưu tiên cao (high priority task).
+ Khu vực ngã tư là tài nguyên sử dụng chung (shared resource).
+ Giả sử tác vụ có mức độ ưu tiên thấp hơn (low priority task) đã có được chìa khóa để truy cập khu vực được chia sẻ này (shared resource). Nhưng nó không được phép chạy trên CPU vì rất nhiều tác vụ có mức độ ưu tiên trung bình (medium priority tasks) đang chạy trên CPU sẽ không cho phép tác vụ có mức độ ưu tiên thấp hơn chiếm lấy CPU.
+ Bây giờ, khi nhiệm vụ ưu tiên cao hơn đi vào, nó không thể truy cập vào khu vực được chia sẻ này. Bởi vì key đang được giữ để thực hiện bởi low priority task, nhưng low priority task đang không được phép chạy, nó chỉ có thể bỏ key khi nó được phép chạy. Vì vậy, cho đến khi low priority task được phép chạy, key sẽ bị khóa đối với tài nguyên chia sẽ chung này (shared resource) và high priority task không thể truy cập nó.
+ Vì vậy, task có mức độ ưu tiên cao hơn phải đợi cho đến khi task có mức độ ưu tiên thấp hơn giải phóng, gây ra sự đảo ngược trong mức độ ưu tiên.

Trong GPOS, đây hoàn toàn không phải là một vấn đề lớn. Nhưng trong RTOS, nó chắc chắn sẽ dẫn đến các vấn đề bởi vì, bạn đang chặn tác vụ có mức độ ưu tiên cao hơn để thực thi.

Nhưng hầu hết real time kernel thực sử dụng một số kỹ thuật để giải quyết vấn đề này. Vì vậy, RTOS có thể tạo đường dẫn trên không (on the fly) cho phép các tác vụ có mức độ ưu tiên cao hơn vượt qua một tác vụ có mức độ ưu tiên thấp hơn hoặc chúng tôi gọi là rescheduling hoặc có thể có các kỹ thuật khác như temporarily making, để tạo cơ hội cho nhiệm vụ có mức độ ưu tiên thấp nhất chạy và giải phóng khóa.
![alt text](/assets/posts/phan1_rtos/image-11.png)
[create paths on the fly]
![alt text](/assets/posts/phan1_rtos/image-12.png)
[temporarily making]

Tất cả các kỹ thuật này RTOS sử dụng ít nhất để giảm thiểu vấn đề đảo ngược ưu tiên. Priority Inversion hoàn toàn không phải là một vấn đề trong hệ điều hành mục đích chung. Nhưng điều này chắc chắn sẽ gây ra sự cố trong hệ điều hành thời gian thực.
![alt text](/assets/posts/phan1_rtos/image-13.png)

**Những tín năng nào mà RTOS có nhưng GPOS lại không có?**
1. Priority based preemptive scheduling mechanism (Cơ chế lập lịch trước dựa trên mức độ ưu tiên)
Điều đó có nghĩa là nó luôn ưu tiên nhiệm vụ ưu tiên cao nhất trong hệ thống. Nhưng GPOS không thể hoạt động như vậy, nếu nó làm như vậy sẽ giết chết thông lượng (throughput) của hệ thống.
Vì vậy, GPOS thường áp dụng các kỹ thuật scheduling làm tăng throughput của hệ thống. Và điểm tiếp theo là bạn sẽ không tìm thấy các đoạn mã phần Quan trọng rất dài nơi ngắt cũng như quyền ưu tiên của hệ thống bị vô hiệu hóa, để bảo vệ phần quan trọng.
2. No or very short Critical sections which disables the preemption (Không có hoặc rất ngắn Phần quan trọng vô hiệu hóa quyền ưu tiên)
3. Priority inversion avoidance (tránh đảo ngược ưu tiên)
Và trong RTOS tránh đảo ngược ưu tiên là điều bắt buộc. Nếu không, điều đó có thể dẫn đến sự cố của hệ thống. Nhưng trong trường hợp vấn đề đảo ngược ưu tiên GPOS thì không phải là vấn đề nghiêm trọng.
4. Bounded Interrupt latency
5. Bounded Scheduling latency, etc.
Và RTOS luôn có độ trễ ngắt có giới hạn cũng như độ trễ lập lịch có giới hạn. Nhưng trong trường hợp của GPOS, độ trễ ngắt và độ trễ lập lịch tác vụ có thể thay đổi đáng kể do độ phức tạp của hệ thống cũng như do sự gia tăng tải Hệ thống khi thời gian trôi qua.

# 6. What is Multitasking?
Một ví dụ tương tự về Multitasking: một ngày bình thường của bạn có 24 giờ và bạn cố hoàn thành những công việc khác nhau, như là ăn sáng, trả lời email, gọi điện thoại, ghi chú, tham gia cuộc họp, ngủ, … Bạn cố gắng hoàn thành những nhiệm vụ đó nhiều nhất có thể để giữ một ngày của bạn thật năng suất.
![alt text](/assets/posts/phan1_rtos/image-14.png)

**Bạn thực hiện tất cả nhiệm vụ đó bằng cách nào?**

Cách thứ nhất là, bạn chia thời gian cho mỗi nhiệm vụ: 20 phút cho việc ăn sáng, 20 phút để viết email, …

Cách khác là bạn có thể tải công việc lên Bộ phận hỗ trợ để tăng năng suất của mình.
![alt text](/assets/posts/phan1_rtos/image-15.png)

Tương tự trong tính toán đa nhiệm, một ứng dụng có thể bao gồm nhiều tác vụ. Mỗi nhiệm vụ phải thực hiện một chức năng duy nhất.
**Giả sử**: có một ứng dụng gọi là hệ thống theo dõi nhiệt độ và ứng dụng này có 3 nhiệm vụ duy nhất. Task 1: đọc dữ liệu cảm biến, Task2: cập nhật màn hình, Task 3: xử lý các đầu vào của người dùng như nhấn nút, v.v... Ứng dụng này đang thực hiện nhiều tác vụ.
![alt text](/assets/posts/phan1_rtos/image-16.png)

Task có nghĩa là, hãy nghĩ giống như một đoạn mã có thể chạy trên CPU và thực thi. Vì vậy, bây giờ, bạn có một CPU và bạn phải chạy tất cả các tác vụ này.  Vì vậy, làm thế nào để bạn chạy nó?
![alt text](/assets/posts/phan1_rtos/image-17.png)

Một cách là đưa ra một khoảng thời gian nhỏ cho mỗi tác vụ chạy. Giả sử, sau thời gian t_1, hãy loại bỏ Task 1 và thực hiện cho Task 2 chạy, v.v. Để làm điều này, bạn cần một scheduler (bộ lập lịch). Bộ lập lịch là người đảm nhận việc lập lịch cho tất cả tác vụ này lên CPU để thực thi. Trong một kịch bản đa nhiệm, bộ lập lịch cũng đóng một vai trò quan trọng.
![alt text](/assets/posts/phan1_rtos/image-18.png)

Bây giờ một cách khác để chạy tất cả tác vụ này là sử dụng multi-core processor (bộ xử lý đa lõi).
Giả sử bạn có một bộ xử lý (processor) với 4 lõi (core).
![alt text](/assets/posts/phan1_rtos/image-19.png)

Trong trường hợp này, bạn không cần trình lập lịch để chạy ứng dụng này, bởi vì, nó có bốn core và mỗi core có thể thực hiện một nhiệm vụ. Vì thế, tất cả 3 task có thể được thực hiện một cách đồng thời.

Nhưng trong lập trình nhúng, người ta thường không sử dụng bộ xử lý (processor) với nhiều core. Ta thường gặp trường hợp bộ xử lý (processor) một lõi (core) và nhiều task.

Vì vậy, để chạy tất cả các tác vụ này, bạn sẽ cần một scheduler và scheduler sẽ quyết định tác vụ n1ào sẽ sử dụng CPU tiếp theo.

Đây là cách nhiều tác vụ thực thi trên CPU, mang lại cho bạn ảo giác rằng tất cả các tác vụ đang thực thi đồng thời. Ví dụ, trong máy tính để bàn của bạn, bạn thường làm việc với nhiều phần mềm cùng một lúc, phải không?
![alt text](/assets/posts/phan1_rtos/image-20.png)
![alt text](/assets/posts/phan1_rtos/image-21.png)

Tất cả các ứng dụng này sẽ có nhiệm vụ tương ứng là các tiến trình dùng chung CPU. Nhưng hệ điều hành của bạn được thiết kế theo cách, nó mang lại cho bạn cảm giác rằng tất cả các ứng dụng đang chạy đồng thời.