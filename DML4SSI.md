# Table Content

### **PHẦN 1: Đặt vấn đề & Động lực nghiên cứu (Introduction & Motivation)**

⏱ *Thời gian dự kiến: 5 phút*

* **Slide 1: Tiêu đề bài thuyết trình**  
  * Tên paper, tác giả (Chris Hays & Manish Raghavan \- MIT).  
  * Tên người thuyết trình.  
* **Slide 2: Hiện tượng Nhiễu loạn (Interference) trong Suy luận Causal**  
  * Nhắc lại giả định SUTVA truyền thống (giá trị đối xử của đơn vị này không ảnh hưởng đến đơn vị khác).  
  * Thực tế: Sự nhiễu loạn (Interference) xảy ra ở khắp mọi nơi (ví dụ: nền tảng video ngắn, ứng dụng gọi xe, thị trường nhà ở).  
  * Hậu quả: Ước lượng causal bị chệch (biased) nếu bỏ qua nhiễu loạn.  
* **Slide 3: Khái niệm mới: Shared-State Interference (SSI)**  
  * Định nghĩa trực quan: Các đơn vị tương tác với nhau thông qua một "trạng thái chung" (Shared State) như: giá cả, thuật toán gợi ý, thời gian chờ, lượng hàng tồn kho.  
  * Đặc điểm: Đơn vị vừa *bị ảnh hưởng* bởi trạng thái chung, vừa *góp phần làm thay đổi* trạng thái đó.  
* **Slide 4(optional) : Hạn chế của các nghiên cứu trước & Đóng góp của bài báo**  
  * *Trước đây:* Thường dựa vào mô hình parametric (mô hình có tham số cố định) hoặc giả định đặc thù cho từng bài toán cụ thể.  
  * *Đóng góp chính:*  
    1. Đưa ra khung lý thuyết tổng quát (General Framework) cho SSI.  
    2. Mở rộng định lý Double Machine Learning (DML) cho SSI, cho phép dùng ML linh hoạt mà không cần giả định parametric.  
    3. Cung cấp bộ ước lượng phương sai nhất quán (Consistent Variance Estimator) để xây dựng khoảng tin cậy chuẩn xác.

### **PHẦN 2: Mô hình hóa Shared-State Interference (Modeling SSI)**

⏱ *Thời gian dự kiến: 5 phút*

* **Slide 5: Thiết lập mô hình toán học (Setting & Notation)**  
  * Mô tả chuỗi thực thể đến theo thời gian $t \= 1, 2, ..., T$.  
  * Các biến số: Covariates $X\_t$, Biến đối xử $D\_t$, Trạng thái chung $H\_t$, Kết quả $Y\_t$.  
  * Hàm tiềm năng (Potential Outcomes): $Y\_t(D\_t, H\_t)$.  
* **Slide 6: Giả định cốt lõi \- Tính chất Markov (The Markov Property)**  
  * Giả định chính: Trạng thái chung $H\_t$ tại bước tiếp theo độc lập với quá khứ nếu đã biết trạng thái và dữ liệu của bước $t-1$.  
  * Cấu trúc đồ thị phụ thuộc (Dependency Structure): Giải thích sơ đồ mạng lưới liên kết (Hình 1 trong paper) để người nghe thấy dòng chảy dữ liệu.  
* **Slide 7: Các điều kiện của Chuỗi Markov (Assumption 2.1)**  
  * Hệ thống SSI phải thỏa mãn 1 trong 2 điều kiện:  
    * (a) *Geometric ergodicity & Detailed balance* (Hệ thống hội tụ về trạng thái cân bằng ổn định nhanh theo hàm mũ).  
    * (b) *m-dependence* (Các quan sát cách nhau xa hơn $m$ bước thì hoàn toàn độc lập với nhau \- thường dùng trong switchback experiments).

### **PHẦN 3: Lý thuyết Double Machine Learning cho SSI**

⏱ *Thời gian dự kiến: 7 phút*

* **Slide 8: Tổng quan về Double Machine Learning (DML)**  
  * DML giải quyết vấn đề gì? Cho phép ước lượng tham số causal mục tiêu một cách hiệu quả ngay cả khi các tham số phụ (nuisance parameters \- như propensity score) được học bởi các mô hình ML phức tạp (Non-parametric).  
  * Sự khác biệt trong SSI: Không thể chia dữ liệu (Sample Splitting) kiểu iid thông thường vì dữ liệu bị phụ thuộc chuỗi. Giải pháp: Sử dụng dữ liệu phụ trợ (Auxiliary Data) độc lập.  
* **Slide 9: Thuật toán DML cho SSI (Algorithm 1\)**  
  * Bước 1: Huấn luyện mô hình ước lượng hàm phụ (nuisance function) $\\hat{\\eta}$ từ dữ liệu phụ trợ $W^{aux}$.  
  * Bước 2: Xây dựng bộ ước lượng mục tiêu $\\hat{\\psi} \= \\psi(W\_{1:T}, \\hat{\\eta})$.  
* **Slide 10: Các giả định kỹ thuật (Neyman Orthogonality)**  
  * Giải thích ngắn gọn về điều kiện mượt (Smoothness) và tính trực giao Neyman (Neyman Orthogonality): Giúp bộ ước lượng ít nhạy cảm với sai số bậc nhất của mô hình ML.  
* **Slide 11: Định lý chính (Theorem 3.3)**  
  * Khẳng định tính chuẩn tắc tiệm cận (Asymptotic Normality): $\\sqrt{T}\\sigma^{-1}(\\hat{\\psi} \- \\psi^\*) \\rightarrow N(0, 1)$.  
  * Giới thiệu công thức ước lượng phương sai $\\hat{\\sigma}^2$ cho 2 trường hợp (Geometric Ergodicity vs $m$-dependence). Nhấn mạnh: Ước lượng phương sai trong chuỗi Markov không thể dùng công thức cắm (plug-in) thông thường.

### **PHẦN 4: Ứng dụng mô hình thực tế (Instantiations & Applications)**

⏱ *Thời gian dự kiến: 7 phút*

* **Slide 12: Ứng dụng 1 \- Ước lượng Tác động Trực tiếp Trung bình (Average Direct Effect \- ADE)**  
  * Bối cảnh: Dữ liệu quan sát (Observational Data).  
  * Mục tiêu (Estimand): ADE \- Đo lường sự thay đổi kết quả khi đổi trạng thái đối xử của một đơn vị mà giữ nguyên phân phối đối xử của các đơn vị khác.  
  * Cơ chế: Thiết lập bộ ước lượng dạng AIPW (Augmented Inverse Probability Weighting) có điều chỉnh theo trạng thái chung $H\_t$.  
* **Slide 13: Ứng dụng 2 \- Thử nghiệm Switchback cho Tác động Toàn cục (Global Average Treatment Effect \- GATE)**  
  * Bối cảnh: Thử nghiệm Switchback (giao dịch/đối xử được bật/tắt theo các khối thời gian kế tiếp nhau) trong môi trường có nhiễu $m$-dependent.  
  * Mục tiêu (Estimand): GATE \- So sánh khi tất cả các đơn vị được đối xử (Treatment) vs tất cả bị kiểm soát (Control).  
  * Cơ chế: Bộ ước lượng DML kết hợp Regression Adjustment giúp giảm đáng kể phương sai so với phương pháp truyền thống.

### **PHẦN 5: Kết quả Mô phỏng Thực nghiệm (Simulations)**

⏱ *Thời gian dự kiến: 4 phút*

* **Slide 14: Thực nghiệm cho ADE (Kết quả từ Hình 2 & Hình 3\)**  
  * So sánh DML4SSI với các phương pháp ngây thơ (Naive Plug-in, Horvitz-Thompson, Naive DML coi dữ liệu là iid).  
  * *Kết quả độ chệch (Bias):* Các phương pháp ngây thơ bị chệch nặng; DML4SSI hội tụ chính xác về 0\.  
  * *Kết quả độ phủ khoảng tin cậy (Coverage):* Phương pháp xem trạng thái chung như covariate thông thường (SSAC) làm đánh giá thấp phương sai, dẫn đến khoảng tin cậy quá hẹp và độ phủ thấp. DML4SSI đạt tỷ lệ phủ mục tiêu 95%.  
* **Slide 15: Thực nghiệm cho GATE trong Switchback (Kết quả từ Hình 4 & Hình 5\)**  
  * So sánh với bộ ước lượng Switchback chuẩn (Bojinov et al., 2022).  
  * *Điểm vượt trội:* Cả hai đều không chệch, nhưng DML4SSI có **phương sai thấp hơn rõ rệt** (Phân phối nhọn hơn và hẹp hơn), giúp tiết kiệm cỡ mẫu (sample size) thử nghiệm.

### **PHẦN 6: Kết luận & Thảo luận (Discussion & Conclusion)**

⏱ *Thời gian dự kiến: 2 phút*

* **Slide 16: Tóm tắt bài thuyết trình**  
  * SSI là một khung cấu trúc nhiễu loạn thực tế và khả thi để tính toán.  
  * Kết hợp thành công DML vào chuỗi dữ liệu phụ thuộc Markov.  
* **Slide 17: Hướng phát triển tương lai (Future Work)**  
  * Mở rộng sang các hàm mục tiếp khác (ví dụ: Tác động gián tiếp trung bình \- Average Indirect Effect).  
  * Nghiên cứu trường hợp trạng thái chung ngược lại tác động đến việc phân bổ đối xử.  
  * Ứng dụng vào dữ liệu thực tế của các hệ thống khuyến nghị thương mại.  
* **Slide 18: Q\&A**  
  * Lời cảm ơn và mời khán giả đặt câu hỏi.

### **💡 Lời khuyên khi trình bày bài này:**

1. **Nhấn mạnh phần "Shared State"**: Khán giả làm về Causal Inference thường quen với việc nhiễu loạn qua mạng lưới (Network Interference). Hãy nhấn mạnh rằng SSI đại diện cho tương tác thông qua *nền tảng trung gian* (như thuật toán hoặc giá thị trường), giúp đơn giản hóa bài toán từ đồ thị dày đặc sang chuỗi Markov.  
2. **Chuẩn bị kỹ phần Phương sai (Variance Estimator)**: Điểm ăn tiền của toán học trong bài này nằm ở Định lý 3.3 khi họ chứng minh được công thức tính phương sai cho chuỗi dữ liệu phụ thuộc. Sẽ rất tốt nếu bạn giải thích được tại sao công thức tính phương sai iid thông thường lại thất bại ở đây (do bỏ qua hiệp phương sai giữa các bước thời gian).

# Slide Content

- SUTVA  
- Ví dụ vi phạm SUTVA / Hậu quả  
- Shared State Interference  
- (Optional) Hạn chế của những nghiên cứu trước đó  
- Các Settings / Notation  
  - Covariate X\_t  
  - Treatment D\_t  
  - Share State H\_t  
  - Outcome Y\_t  
  - Markov Property  
  - SSI thỏa 1 trong 2:  
    - Geometrics ergodicity & Detail Balance  
    - M\_dependency  
- Lý thuyết về DML  
- DML cho SSI  
- Theorem 3.3  
- ADE / GATE  
- Simulations  
- Kết luận

# Slide Script

# Slide 5

Slide này là cánh cửa bước từ phần đặt vấn đề mang tính trực quan sang khung lý thuyết toán học chính thức của bài báo. Khán giả cần phải nắm cực kỳ vững các ký hiệu và dòng chảy thời gian ở slide này để có thể hiểu được các thuật toán và định lý phức tạp ở phía sau.

### **Kịch bản thuyết trình chi tiết cho Slide 5**

#### **1\. Dẫn nhập: Định hình ngôn ngữ toán học cho bài toán**

\*"Thưa các bạn, ở phần mở đầu, chúng ta đã cùng nhau thảo luận về khái niệm hiện tượng nhiễu loạn trạng thái chung (SSI) thông qua các ví dụ thực tế như thuật toán gợi ý hay giá cả thị trường. Vậy làm thế nào để chúng ta dịch chuyển các bài toán thực tế đó thành một ngôn ngữ toán học chuẩn chỉnh để máy tính có thể xử lý và tính toán? \*  
*Slide 5 này chính là nơi các tác giả thiết lập cấu trúc mô hình hóa và các ký hiệu toán học cốt lõi cho toàn bộ nghiên cứu."*

#### **2\. Cấu trúc chuỗi thời gian (Temporal Structure)**

\*"Đầu tiên, mô hình SSI được thiết kế dựa trên một chuỗi thực thể đến theo thời gian, ký hiệu từ $t \= 1, 2, \\dots, T$. \*  
*Các bạn có thể hình dung mỗi bước thời gian $t$ đại diện cho một phiên tương tác. Ví dụ: tại thời điểm $t$, một người dùng truy cập vào TikTok, hoặc một hành khách mở ứng dụng Grab để tìm xe. Toàn bộ tiến trình lịch sử của hệ thống sẽ được ghi nhận dọc theo trục thời gian tuyến tính này."*

#### **3\. Các biến số quan sát tại mỗi bước thời gian (Data Vectors)**

*"Tại mỗi bước thời gian $t$, hệ thống của chúng ta thu thập và ghi nhận một bộ bốn biến số quan sát, ký hiệu là cụm dữ liệu $W\_t$. Bộ bốn này bao gồm:*

* **Thứ nhất, $X\_t$ (Covariates):** *Đây là các đặc trưng nền cảnh hoặc thông tin nền của thực thể tại thời điểm $t$. Ví dụ như vị trí địa lý của khách hàng, lịch sử xem video của người dùng, hay loại thiết bị họ đang sử dụng.*  
  * **Thứ hai, $D\_t$ (Treatment Assignment):** *Đây là biến đối xử nhị phân hoặc đa trị được chỉ định cho thực thể. Ví dụ: hệ thống có quyết định bật tính năng thử nghiệm mới cho người dùng này không, hoặc tài xế có được nhận mã khuyến mãi hay không ($D\_t \\in \\{0, 1\\}$).*  
  * **Thứ ba, $H\_t$ (Shared State):** *Đây chính là **Trạng thái chung** của hệ thống tại thời điểm $t$. Đây là biến số mang tính quyết định của toàn bộ paper. Nó đại diện cho môi trường trung gian mà các thực thể tương tác qua đó — ví dụ: mức độ tắc nghẽn của mạng lưới giao thông, trạng thái phân phối của kho hàng, hoặc phân phối trọng số của thuật toán gợi ý hiện tại.*  
  * **Thứ tư, $Y\_t$ (Outcome):** *Là kết quả đo lường cuối cùng mà chúng ta quan tâm sau khi thực thể tương tác với hệ thống. Ví dụ: người dùng có nhấn vào xem video hay không, hoặc cuốc xe có được thực hiện thành công hay không."*

#### **4\. Hàm Kết quả Tiềm năng (Potential Outcomes Framework) dưới tác động của SSI**

*"Từ các biến số trên, các tác giả mở rộng khung lý thuyết Kết quả Tiềm năng (Potential Outcomes) của Rubin để định nghĩa hàm kết quả dưới dạng:*  
$$Y\_t(D\_t, H\_t)$$  
*Các bạn hãy chú ý kỹ vào đối số của hàm này. Trong mô hình causal inference truyền thống (SUTVA), kết quả $Y\_t$ chỉ phụ thuộc vào đối xử của chính cá thể đó, tức là $Y\_t(D\_t)$. Nhưng trong môi trường Shared-State Interference, kết quả tiềm năng của cá thể $t$ bị đồng quyết định bởi **hai yếu tố**: hành vi đối xử trực tiếp lên chính họ ($D\_t$), và **trạng thái chung của toàn hệ thống** tại thời điểm đó ($H\_t$).*  
*Điều này phản ánh chính xác thực tế: Ngay cả khi bạn nhận được mã giảm giá ($D\_t=1$), nhưng nếu trạng thái chung của hệ thống lúc đó là không có tài xế nào trống ở xung quanh ($H\_t$ ở trạng thái cạn kiệt), thì kết quả là bạn vẫn không thể đặt được xe ($Y\_t=0$)."*

#### **5\. Cơ chế tương tác hai chiều (The Feedback Loop)**

*"Điểm đặc biệt cuối cùng của thiết lập này là mối quan hệ nhân quả hai chiều diễn ra theo thời gian:*

* *Trạng thái chung hiện tại $H\_t$ sẽ tác động đến kết quả $Y\_t$ của thực thể hiện tại.*  
* *Ngược lại, hành vi $D\_t$ và đặc trưng $X\_t$ của thực thể hiện tại, sau khi tương tác xong, sẽ đóng góp một phần nhỏ làm thay đổi và cập nhật trạng thái chung cho bước tiếp theo $H\_{t+1}$.*

*Chính vòng lặp phản hồi (feedback loop) liên tục này tạo ra sự phụ thuộc chuỗi phức tạp của dữ liệu, khiến cho các giả định độc lập đồng phân phối (iid) truyền thống hoàn toàn bị sụp đổ."*

#### **6\. Chuyển ý (Kết thúc Slide)**

*"Khi đã có trong tay đầy đủ các định nghĩa và ký hiệu toán học này, câu hỏi tiếp theo là: Chúng ta cần những giả định gì về mặt cấu trúc để có thể kiểm soát và giải được vòng lặp phụ thuộc phức tạp này? Chúng ta hãy cùng chuyển sang Slide 6 để tìm hiểu về Giả định thuộc tính Markov của hệ thống."*

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Liên kết ký hiệu với sơ đồ:** Slide này nên có một sơ đồ đồ thị dạng dòng chảy (ví dụ: $H\_t \\rightarrow Y\_t \\leftarrow D\_t$, rồi mũi tên từ $(D\_t, X\_t, H\_t) \\rightarrow H\_{t+1}$). Khi thuyết trình, hãy dùng con trỏ vừa nói vừa chỉ theo các mũi tên của sơ đồ để khán giả dễ dàng ghi nhớ ký hiệu.  
* **Nhấn mạnh sự khác biệt với SUTVA:** Hãy nói rõ cụm từ **"Hàm kết quả phụ thuộc vào hai đối số"**. Đây là cốt lõi toán học phân tách bài báo này với các nghiên cứu causal inference cơ bản.  
* **Tốc độ nói:** Hãy nói tương đối chậm ở slide này. Đây là slide định nghĩa ký hiệu, nếu bạn đi quá nhanh và khán giả bị "rớt" lại không nhớ $H\_t$ hay $W\_t$ là gì, họ sẽ hoàn toàn bị lạc lối ở các slide thuật toán (Slide 9\) và định lý (Slide 11\) tiếp theo.

# Slide 6

Dưới đây là kịch bản thuyết trình chi tiết cho **Slide 6: Giả định cốt lõi \- Tính chất Markov (The Markov Property)**.  
Slide này giải quyết một câu hỏi cực kỳ quan trọng: *Làm sao để kiểm soát vòng lặp phản hồi phức tạp đã thiết lập ở Slide 5 mà không làm mô hình bị quá tải toán học?* Đây chính là chìa khóa giúp bài toán trở nên khả thi (tractable).

### **Kịch bản thuyết trình chi tiết cho Slide 6**

#### **1\. Dẫn nhập: Thu hẹp không gian phụ thuộc**

"Thưa các bạn, ở Slide 5 chúng ta đã thấy một vòng lặp phản hồi vô cùng phức tạp: hành vi của thực thể hôm nay thay đổi trạng thái ngày mai, trạng thái ngày mai lại ảnh hưởng đến thực thể ngày kia, tạo ra một mạng lưới phụ thuộc dày đặc theo thời gian. Nếu mọi điểm trong quá khứ đều ảnh hưởng đến hiện tại, mô hình toán học sẽ bị quá tải và không thể giải được trong thực tế.  
Chính vì vậy, Slide 6 này giới thiệu **Giả định cốt lõi** giúp đơn giản hóa toàn bộ bài toán nhưng vẫn giữ trọn vẹn bản chất thực tế: đó là **Tính chất Markov của Trạng thái chung (Shared-State Markov Property)**."

#### **2\. Phát biểu Giả định Toán học: Công thức (1)**

"Mời các bạn nhìn vào công thức xác suất điều kiện (1) trên slide:  
$$\\mathbb{P}(H\_t \\in A \\mid W\_{1:(t-1)}) \= \\mathbb{P}(H\_t \\in A \\mid W\_{t-1})$$  
Phát biểu bằng ngôn ngữ thống kê, các tác giả giả định rằng: Nếu chúng ta đã biết toàn bộ thông tin của bước thời gian ngay trước đó — ký hiệu là $W\_{t-1}$ — thì trạng thái chung $H\_t$ tại bước hiện tại sẽ hoàn toàn độc lập điều kiện với toàn bộ lịch sử dữ liệu trong quá khứ xa hơn, từ $W\_1$ cho đến $W\_{t-2}$.  
Nói một cách dễ hiểu: **'Quá khứ xa xôi đã được gói gọn hoàn toàn trong hiện tại'**. Trạng thái chung của hệ thống chỉ quan tâm đến những gì vừa xảy ra ở bước liền trước, chứ không cần nhớ lại lịch sử từ thuở sơ khai."

#### **3\. Ví dụ thực tế minh họa cho giả định**

"Để thấy giả định này hợp lý như thế nào trong thực tế, chúng ta hãy lấy ví dụ về một thị trường thương mại điện tử hoặc một nền tảng gọi xe công nghệ:

* Lượng hàng tồn kho hoặc số lượng tài xế trống tại thời điểm $t$ ($H\_t$) chính là bằng lượng tồn kho ở thời điểm liền trước ($H\_{t-1}$), trừ đi hoặc cộng thêm dựa trên việc khách hàng ở bước thời gian $t-1$ có thực hiện giao dịch hay không ($W\_{t-1}$).  
* Hệ thống không cần biết khách hàng từ 3 tiếng trước đã mua gì; mọi tác động của người dùng trong quá khứ đã được tích lũy và phản ánh trực tiếp vào con số tồn kho hiện tại rồi."\*

#### **4\. Phân tích Sơ đồ cấu trúc phụ thuộc (Hình 1 \- Dependency Structure)**

"Xin mời các bạn nhìn vào sơ đồ đồ thị Hình 1 được trích xuất từ paper để thấy dòng chảy nhân quả hoạt động tường minh thế nào dưới giả định này:

* Các bạn có thể thấy các mũi tên từ quá khứ đi sang tương lai bắt buộc phải **'đi xuyên qua'** các nút trạng thái chung $H\_{t-1}$ và $H\_t$.  
* Nhiễu loạn (Interference) xảy ra theo trục dọc: Đặc trưng cá thể $X\_{t-1}$ và biến đối xử $D\_{t-1}$ tác động trực tiếp lên kết quả $Y\_{t-1}$ của chính họ, đồng thời bắn một mũi tên lên trên để cập nhật trạng thái chung tiếp theo $H\_t$.  
* Và tại bước thời gian $t$, trạng thái chung mới $H\_t$ lại bắn một mũi tên đi xuống để cùng với $X\_t$ và $D\_t$ quyết định kết quả $Y\_t$.

Sơ đồ này cho thấy: Mặc dù các cá thể không hề tương tác trực tiếp với nhau (không có mũi tên ngang nào nối từ $X\_{t-1}$ sang $X\_t$ hay từ $Y\_{t-1}$ sang $Y\_t$), nhưng họ lại ảnh hưởng chặt chẽ đến nhau một cách gián tiếp thông qua 'trung gian' là đường trạng thái chung nằm ở tầng trên cùng."

#### **5\. Hệ quả lý thuyết: Chuỗi Markov thuần nhất (Homogeneous Markov Chain)**

"Một hệ quả rất đẹp về mặt toán học từ thiết lập này là: Do tính chất Markov của $H\_t$, kết hợp với việc các đặc trưng cá thể $X\_t$ được rút độc lập đồng phân phối (iid), toàn bộ chuỗi quan sát $\\{W\_t\\}\_{t=1}^{\\infty}$ cấu thành một **Chuỗi Markov thuần nhất (Homogeneous Markov Chain)** trên không gian trạng thái tổng quát.  
Điều này cho phép các tác giả định nghĩa một Kernel chuyển trạng thái $K\_H$ cố định theo thời gian (như công thức 2.1 trên slide). Đây chính là nền móng lý thuyết vững chắc giúp chúng ta áp dụng các định lý giới hạn trung tâm của chuỗi Markov ở các slide sau nhằm tính toán phương sai một cách chính xác."

#### **6\. Chuyển ý (Kết thúc Slide)**

"Tóm lại, tính chất Markov chính là 'mẹo toán học' giúp biến một bài toán nhiễu loạn dày đặc phức tạp thành một chuỗi các bước chuyển đổi có cấu trúc và tính toán được. Tuy nhiên, để chuỗi Markov này vận hành ổn định lâu dài tiệm cận về một trạng thái cân bằng, nó cần thỏa mãn một số điều kiện kỹ thuật tự nhiên. Chúng ta hãy cùng sang Slide 7 để tìm hiểu về các điều kiện ổn định này."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Tận dụng sơ đồ Hình 1:** Khi giải thích phần 4, hãy dùng con trỏ chuột hoặc laser chỉ trực tiếp vào các mũi tên trong Hình 1 theo đúng thứ tự thời gian: Chỉ vào $W\_{t-1} \\rightarrow H\_t \\rightarrow Y\_t$. Khán giả sẽ hiểu ngay lập tức khái niệm *"nhiễu loạn được trung hòa qua trạng thái chung"* mà không cần đọc công thức xác suất phức tạp.  
* **Nhấn mạnh cụm từ "Độc lập điều kiện" (Conditionally Independent):** Đây là thuật ngữ chuẩn của ngành Causal Inference. Hãy nói rõ rằng: Dữ liệu bị phụ thuộc, nhưng nhờ có $H\_{t-1}$ và $W\_{t-1}$, chúng trở nên độc lập điều kiện, giúp bẻ gãy sự ràng buộc vô hạn của quá khứ.  
* **Giọng điệu giải thích:** Hãy giữ một tông giọng giải thích mang tính khai sáng, vì đây là phân đoạn gỡ nút thắt cho sự phức tạp đã đặt ra ở Slide 5\.

# Slide 7

Dưới đây là kịch bản thuyết trình chi tiết cho **Slide 7: Các điều kiện của Chuỗi Markov (Assumption 2.1)**.  
Slide này đóng vai trò thiết lập nền tảng kỹ thuật toán học để giải quyết vòng lặp phụ thuộc phức tạp mà chúng ta vừa thảo luận ở Slide 5 và Slide 6\. Mục tiêu của bạn ở slide này là giải thích cho khán giả hiểu **hai kịch bản toán học** mà hệ thống cần thỏa mãn để các định lý Double ML ở phía sau có hiệu lực.

### **Kịch bản thuyết trình chi tiết cho Slide 7**

#### **1\. Dẫn nhập: Biến bài toán vô hạn thành có thể giải được**

\*"Thưa các bạn, ở Slide 5 và 6, chúng ta đã thấy một vòng lặp phản hồi vô hạn giữa trạng thái chung $H\_t$ và kết quả $Y\_t$ dọc theo trục thời gian tuyến tính. Về mặt lý thuyết, nếu mỗi bước thời gian đều phụ thuộc vào toàn bộ quá khứ xa xôi, bài toán suy luận causal sẽ trở nên bất khả thi vì lượng thông tin cần xử lý là vô hạn. \*  
Để làm cho khung lý thuyết này trở nên khả thi về mặt tính toán (tractable), các tác giả đã đưa ra **Giả định 2.1 (Assumption 2.1)**. Giả định này yêu cầu toàn bộ chuỗi quan sát $W\_{1:\\infty}$ phải thỏa mãn ít nhất một trong hai điều kiện toán học sau đây để kiểm soát tốc độ mất đi của sự phụ thuộc chuỗi."

#### **2\. Điều kiện thứ nhất: Tính công bằng hình học và Cân bằng chi tiết (Geometric Ergodicity & Detailed Balance)**

"Kịch bản đầu tiên, ký hiệu là **Điều kiện (a)**, áp dụng cho các hệ thống hoạt động liên tục và có tính chất hội tụ dài hạn. Ở đây chúng ta có hai khái niệm chính:

* **Tính công bằng hình học (Geometric Ergodicity):** Nói một cách dễ hiểu, đây là sự mở rộng của tính bất khả quy (irreducibility) và tính vô chu kỳ (aperiodicity) từ chuỗi Markov hữu hạn sang không gian trạng thái vô hạn. Nó đảm bảo rằng bất kể hệ thống bắt đầu từ một trạng thái ban đầu hỗn loạn hay cực đoan đến mức nào, chuỗi Markov sẽ hội tụ về một **trạng thái dừng duy nhất (unique stationary distribution)**, ký hiệu là $K^{\\infty}$. Và tốc độ hội tụ này diễn ra **cực kỳ nhanh theo hàm mũ (geometric mixing rate)**.  
  * **Tính cân bằng chi tiết (Detailed Balance):** Mối quan hệ toán học được thể hiện qua công thức (2.2) trên slide:  
  * $$K^{\\infty}(dw)K(w,dz) \= K^{\\infty}(dz)K(z,dw)$$  
* Ý nghĩa trực quan của biểu thức này là tính đảo ngược thời gian (time-reversibility) ở trạng thái dừng. Mật độ xác suất hệ thống đang ở trạng thái $w$ rồi chuyển sang $z$ phải bằng đúng mật độ xác suất hệ thống đang ở $z$ rồi chuyển ngược về $w$.  
* **Tại sao điều kiện này quan trọng?** Nó đảm bảo rằng tác động nhiễu loạn của một cá thể ở quá khứ xa xôi sẽ bị triệt tiêu và phai nhạt dần theo thời gian. Mối tương quan giữa các quan sát cách xa nhau sẽ giảm về 0 đủ nhanh để các định lý giới hạn trung tâm dành cho chuỗi phụ thuộc có thể hoạt động."

#### **3\. Điều kiện thứ hai: Tính phụ thuộc hữu hạn ($m$-dependence)**

"Nếu hệ thống của các bạn không thỏa mãn điều kiện hội tụ dài hạn theo hàm mũ ở trên, các tác giả cung cấp một lối đi thay thế, đó là **Điều kiện (b) \- Tính phụ thuộc hữu hạn ($m$-dependence)**.  
*Biểu thức toán học số (2.3) định nghĩa rất rõ ràng:*  
$$W\_1, \\dots, W\_t \\perp\\\!\\\!\\\!\\perp W\_{t+m+1}, \\dots, W\_T$$

* **Giải thích trực quan:** Điều này có nghĩa là bất kỳ hai cụm dữ liệu nào cách nhau xa hơn một khoảng cố định $m$ bước thời gian thì hoàn toàn độc lập với nhau. Quá khứ chỉ có thể ảnh hưởng đến tương lai trong phạm vi tối đa là $m$ bước.\*  
* **Ứng dụng thực tế:** Giả định $m$-dependence này chính là nền tảng cốt lõi của toàn bộ các nghiên cứu và ứng dụng về **Thử nghiệm Switchback** trong công nghiệp hiện nay. Ví dụ, trong một thị trường giao đồ ăn, một quyết định bật khuyến mãi ở khung giờ này chỉ có thể làm ảnh hưởng đến lượng tài xế bận rộn trong vòng tối đa $m \= 5$ cuốc xe tiếp theo; sau đó, thị trường hoàn toàn tự thiết lập lại và các cuốc xe sau đó độc lập với quá khứ."

#### **4\. Chốt ý: Chuẩn bị cho các bước ước lượng phía sau**

\*"Tóm lại, việc hệ thống thỏa mãn một trong hai điều kiện của Giả định 2.1 là 'tấm vé thông hành' về mặt lý thuyết. Nó cho phép các tác giả chứng minh được rằng, dù dữ liệu có bị nhiễu loạn chuỗi, chúng ta vẫn có thể áp dụng các kỹ thuật Double Machine Learning để bóc tách tác động causal một cách chính xác. \*  
Tương ứng với hai điều kiện (a) và (b) này, lát nữa ở Slide 11, chúng ta cũng sẽ thấy hai công thức toán học hoàn toàn khác nhau để ước lượng phương sai nhất quán cho hệ thống."

#### **5\. Chuyển ý (Kết thúc Slide)**

"Bây giờ, khi khung thiết lập mô hình và các giả định nền tảng về chuỗi Markov đã hoàn thiện, chúng ta đã sẵn sàng bước sang Phần 3 của bài thuyết trình, nơi chúng ta chính thức tìm hiểu cách tích hợp Double Machine Learning vào cấu trúc Shared-State Interference này."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Đơn giản hóa thuật ngữ:** Những từ như *Harris ergodic Markov chain* hay *Detailed balance* rất dễ làm khán giả "choáng váng". Hãy tập trung giải thích phần ý nghĩa trực quan: (a) là **"hội tụ và phai nhạt nhiễu nhanh theo hàm mũ"**, còn (b) là **"nhiễu chỉ kéo dài tối đa $m$ bước rồi biến mất"**.  
* **Liên kết với các slide sau:** Việc liên tục nhắc khán giả rằng *"gi giả định này sẽ làm tiền đề cho công thức tính phương sai ở Slide 11"* giúp bài thuyết trình của bạn có tính liên kết logic cực kỳ chặt chẽ. Khán giả sẽ hiểu tại sao họ cần phải nghe phần lý thuyết này.  
* **Ngôn ngữ cơ thể:** Khi giải thích về $m$-dependence, bạn có thể dùng tay ra hiệu một khoảng cách trên không trung để biểu thị "khoảng cách $m$ bước", giúp người nghe dễ dàng hình dung sự phân tách độc lập giữa các khối dữ liệu.

# Slide 8

Dưới đây là kịch bản thuyết trình chi tiết cho **Slide 8: Tổng quan về Double Machine Learning (DML)**.  
Slide này là phần chuyển giao quan trọng, đưa khán giả bước vào chương trọng tâm của bài báo: Khung lý thuyết **Double Machine Learning áp dụng cho cấu trúc dữ liệu nhiễu loạn (SSI)**. Mục tiêu của bạn ở slide này là làm rõ hai thứ: **DML giải quyết được gốc rễ vấn đề gì** và **tại sao việc đưa DML vào SSI lại là một thách thức lớn**.

### **Kịch bản thuyết trình chi tiết cho Slide 8**

#### **1\. Dẫn nhập: Mở ra giải pháp hiện đại cho bài toán phức tạp**

\*"Thưa các bạn, sau khi đã định hình được cấu trúc toán học và các giả định Markov ở Phần 2, câu hỏi tiếp theo và cũng là thách thức lớn nhất đối với một nhà thực hành dữ liệu là: **Làm sao để ước lượng chính xác tác động nhân quả khi các hàm số trong hệ thống quá phức tạp và phi tuyến tính?**  
Nếu chúng ta bắt buộc hệ thống phải tuân theo các mô hình hồi quy tuyến tính (parametric) kiểu cũ, ước lượng thu được sẽ rất dễ bị chệch do mô hình hóa sai thực tế. Chính vì vậy, ở Phần 3 này, các tác giả đã tìm đến một 'vũ khí hạng nặng' trong thống kê hiện đại: **Double Machine Learning (DML)**."\*

#### **2\. Bản chất của Double Machine Learning (DML) là gì?**

\*"Đầu tiên, tôi xin phép nhắc lại một chút về bản chất của DML, một meta-algorithm được giới thiệu bởi giáo sư Chernozhukov và các cộng sự vào năm 2018\.  
Về mặt ý tưởng, DML cho phép chúng ta sử dụng **bất kỳ thuật toán Machine Learning linh hoạt nào** — như Random Forest, Gradient Boosting, hay Neural Networks — để đi học các tham số phụ (gọi là *nuisance parameters*), ví dụ như hàm propensity score hay hàm kỳ vọng kết quả.  
Thông thường, các mô hình ML này hội tụ rất chậm và có độ chệch lớn trong mẫu nhỏ. Nhưng DML giải quyết triệt để vấn đề này bằng cách kết hợp hai thành phần: **Sample Splitting (Chia mẫu)** để tránh quá khớp (overfitting), và **Bias Correction (Sửa sai)** thông qua một hàm score đặc biệt để triệt tiêu các sai số bậc nhất của mô hình ML. Kết quả là chúng ta vừa tận dụng được độ linh hoạt của ML, vừa giữ được tốc độ hội tụ căn bậc hai của mẫu ($\\sqrt{T}$) để làm suy luận thống kê chính xác."\*

#### **3\. Thách thức lớn: Tại sao DML thông thường lại 'thất thủ' trước SSI?**

\*"Tuy nhiên, định lý DML nguyên bản của năm 2018 được thiết kế dựa trên một giả định cốt lõi: **Dữ liệu phải độc lập và đồng phân phối (iid)**.  
Khi bước vào môi trường Shared-State Interference (SSI), giả định iid này hoàn toàn sụp đổ. Như chúng ta đã phân tích ở Slide 5, dữ liệu bị phụ thuộc nặng nề theo chuỗi thời gian qua cấu trúc Markov của trạng thái chung $H\_t$.  
Sự phụ thuộc này dẫn đến một hệ quả nghiêm trọng: **Chúng ta không thể áp dụng kỹ thuật chia mẫu (Sample Splitting) thông thường được nữa**. Nếu bạn chia dữ liệu thành $k$ phần theo kiểu iid, các phần dữ liệu này vẫn liên đới và 'nói chuyện' với nhau qua dòng chảy thời gian. Hệ quả là mô hình ML huấn luyện trên phần này sẽ không hề độc lập với phần dữ liệu dùng để ước lượng tác động causal, khiến cho các lý thuyết toán học bảo vệ DML bị vô hiệu hóa hoàn toàn."\*

#### **4\. Giải pháp sáng tạo của bài báo: Dữ liệu phụ trợ (Auxiliary Data)**

\*"Để gỡ nút thắt này, các tác giả đã đưa ra một hướng tiếp cận thay thế thông minh, lấy cảm hứng từ các nghiên cứu tiên tiến gần đây. Thay vì cố gắng chia một chuỗi dữ liệu phụ thuộc thành các phần nhỏ, họ giả định chúng ta có quyền truy cập vào một **Tập dữ liệu phụ trợ độc lập (Auxiliary Data Sample)**, ký hiệu là $W^{aux}$.

* **Quy trình mới:** Toàn bộ các mô hình Machine Learning linh hoạt dùng để học các hàm phụ (nuisance functions) sẽ được quăng sang và huấn luyện biệt lập trên tập dữ liệu phụ trợ $W^{aux}$ này.  
* **Kết quả:** Sau khi mô hình ML đã học xong, chúng ta mang các 'tri thức' đã đóng gói đó áp dụng vào tập dữ liệu chính $W\_{1:T}$ để tính toán bộ ước lượng mục tiêu. Do $W^{aux}$ hoàn toàn độc lập với chuỗi dữ liệu chính, tính chất độc lập giữa mô hình phụ và dữ liệu ước lượng được khôi phục, mở đường cho việc chứng minh các định lý hội tụ sau đó."\*

#### **5\. Chuyển ý (Kết thúc Slide)**

\*"Tóm lại, Slide 8 đã vạch ra một lộ trình tư duy rõ ràng: Chúng ta muốn dùng ML để xử lý cấu trúc phức tạp của SSI, nhưng để làm được điều đó một cách an toàn về mặt toán học, chúng ta phải thay đổi cơ chế chia mẫu truyền thống bằng giải pháp Dữ liệu phụ trợ.  
Ngay sau đây, ở Slide 9, chúng ta sẽ cùng xem các bước vận hành chi tiết của Thuật toán 1 cụ thể hóa ý tưởng này như thế nào."\*

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Nhấn mạnh từ "Nút thắt" (The Bottleneck):** Hãy làm cho khán giả thấy sự kịch tính ở đoạn *"Tại sao DML thông thường lại thất thủ"*. Việc nêu bật thách thức lý thuyết (sự sụp đổ của kỹ thuật Sample Splitting do dữ liệu phụ thuộc chuỗi) sẽ làm tăng giá trị cho giải pháp sáng tạo của các tác giả ở vế sau.  
* **Liên hệ thực tế về dữ liệu phụ trợ:** Để khán giả dễ hình dung, bạn có thể nói: *"Trong thực tế, tập dữ liệu phụ trợ $W^{aux}$ này có thể hiểu đơn giản là dữ liệu vận hành của tuần trước, còn tập dữ liệu chính $W\_{1:T}$ là chuỗi dữ liệu của tuần này khi chúng ta tiến hành ước lượng"*.  
* **Tông giọng:** Thể hiện sự rõ ràng, mạch lạc vì đây là slide mang tính chất "bản lề" về mặt tư duy, giúp người nghe hiểu *tại sao* các tác giả lại thiết kế thuật toán ở Slide 9 theo cách như vậy.

# Slide 9

Để thuyết trình phần **Slide 9: Thuật toán DML cho SSI (Algorithm 1\)**, bạn cần truyền tải được sự thay đổi trong quy trình xử lý dữ liệu so với Double Machine Learning (DML) truyền thống. Trong môi trường SSI, chúng ta không thể "trộn" dữ liệu một cách ngẫu nhiên.  
Dưới đây là kịch bản thuyết trình chi tiết cho Slide 9:

### **Kịch bản thuyết trình cho Slide 9**

#### **1\. Dẫn nhập: Tại sao DML truyền thống không dùng được?**

\*"Ở slide trước, chúng ta đã nhắc đến DML. Trong DML chuẩn (cho dữ liệu i.i.d), chúng ta thường dùng phương pháp **Sample Splitting** (chia đôi dữ liệu): một nửa dùng để huấn luyện mô hình ước lượng biến phụ (nuisance), nửa còn lại dùng để tính toán tác động causal.  
Tuy nhiên, với **Shared-State Interference (SSI)**, dữ liệu của chúng ta là một chuỗi có phụ thuộc thời gian ($H\_t$ phụ thuộc $H\_{t-1}$). Nếu chúng ta chia mẫu ngẫu nhiên, chúng ta sẽ phá vỡ cấu trúc Markov này. Do đó, thuật toán DML cho SSI (Algorithm 1\) cần một cách tiếp cận khác: sử dụng **dữ liệu phụ trợ (Auxiliary Data)** hoặc **kỹ thuật chia block**."\*

#### **2\. Giải thích các bước của Thuật toán 1**

*"Thuật toán này bao gồm hai giai đoạn chính để đảm bảo tính trực giao (orthogonality) và loại bỏ bias từ các mô hình học máy phức tạp:"*

* **Bước 1: Ước lượng các hàm phụ (Nuisance Estimation)**  
* \*"Đầu tiên, chúng ta ước lượng các hàm phụ $\\hat{\\eta} \= (\\hat{q}, \\hat{m})$, trong đó $\\hat{q}$ là mô hình dự báo trạng thái chung và $\\hat{m}$ là mô hình dự báo kết quả tiềm năng.  
* Điểm khác biệt quan trọng ở đây là thay vì dùng toàn bộ dữ liệu, chúng ta huấn luyện trên một tập **Auxiliary Data** (dữ liệu phụ trợ) hoặc sử dụng kỹ thuật **Cross-fitting theo khối (Block Cross-fitting)**. Việc này đảm bảo rằng sai số của mô hình $\\hat{\\eta}$ tại thời điểm $t$ không bị 'lây lan' sang bước tính toán tác động causal tại chính thời điểm đó."\*  
* **Bước 2: Xây dựng bộ ước lượng mục tiêu (Target Estimator)**  
* \*"Sau khi đã có $\\hat{\\eta}$, chúng ta bước sang giai đoạn tính toán giá trị mục tiêu $\\hat{\\psi}$. Tại đây, chúng ta sử dụng hàm **Score Function** (hay còn gọi là hàm ảnh hưởng \- influence function) đã được thiết kế riêng cho SSI.  
* Công thức $\\hat{\\psi} \= \\psi(W\_{1:T}, \\hat{\\eta})$ ở đây thực chất là lấy trung bình của hàm số điểm (score) qua toàn bộ chuỗi thời gian $T$. Hàm score này có tính chất **Neyman Orthogonal**, nghĩa là đạo hàm của nó đối với các tham số phụ $\\eta$ tại giá trị thực bằng 0\. Nhờ đó, sai số nhỏ trong mô hình ML của chúng ta sẽ không làm chệch đi kết quả cuối cùng."\*

#### **3\. Điểm nhấn kỹ thuật (Key Takeaways)**

*"Các bạn hãy chú ý ba yếu tố giúp thuật toán này thành công:"*

* **Decoupling (Tách rời):** *Việc tách rời quá trình học nuisance và quá trình ước lượng $\\psi$ giúp ta sử dụng được các mô hình ML hiện đại (như Neural Networks hay Gradient Boosting) mà không sợ bị overfitting hay bias.*  
* **Sequential Dependency (Phụ thuộc tuần tự):** *Thuật toán không giả định các quan sát độc lập, mà nó tích hợp cấu trúc của trạng thái chung $H\_t$ vào hàm score để 'làm sạch' nhiễu.*  
* **Auxiliary Data:** *Nếu hệ thống quá phụ thuộc, chúng ta dùng một tập dữ liệu phụ để huấn luyện $\\hat{\\eta}$, điều này giúp bộ ước lượng $\\hat{\\psi}$ đạt được tính tiệm cận chuẩn.*

### **Mẹo cho người thuyết trình:**

* **Sử dụng Sơ đồ:** Khi nói đến "dữ liệu phụ trợ" và "dữ liệu mục tiêu", hãy chỉ vào sơ đồ luồng dữ liệu trên Slide 9\.  
* **Trả lời câu hỏi phản biện (nếu có):** Nếu ai đó hỏi "Tại sao không dùng K-fold Cross-fitting thông thường?", bạn hãy trả lời ngay: *"Vì trong SSI, $Y\_t$ phụ thuộc vào $H\_{t-1}$. K-fold thông thường sẽ làm xáo trộn thứ tự thời gian và phá vỡ mối quan hệ Markov này, dẫn đến ước lượng sai lệch phương sai."*  
* **Kết nối:** Kết thúc slide này bằng cách nói: *"Sau khi đã có thuật toán này, câu hỏi tiếp theo là: Làm sao để biết khoảng tin cậy của nó rộng bao nhiêu? Chúng ta sẽ giải đáp ở Slide 11 về Định lý chuẩn tắc tiệm cận."*

# Slide 10

### **Kịch bản thuyết trình chi tiết cho Slide 10**

#### **1\. Dẫn nhập: Đi sâu vào cơ chế "Miễn nhiễm sai số"**

"Thưa các bạn, ở Slide 9 chúng ta đã nói rằng Thuật toán DML có một cơ chế đặc biệt giúp nó 'miễn nhiễm' với sai số của các mô hình Machine Learning phụ trợ. Vậy cơ chế đó hoạt động như thế nào về mặt toán học? Slide 10 này chính là câu trả lời, giới thiệu hai khái niệm kỹ thuật cốt lõi: **Đạo hàm Gateaux (Gateaux derivative)** và **Tính trực giao Neyman (Neyman Orthogonality)**."

#### **2\. Khái niệm 1: Đạo hàm Gateaux (Gateaux Derivative)**

"Đầu tiên là **Đạo hàm Gateaux** (Định nghĩa A.1). Các bạn có thể hình dung nó giống như đạo hàm thông thường trong giải tích, nhưng thay vì đo lường sự thay đổi của một hàm số theo một biến số, đạo hàm Gateaux đo lường **mức độ nhạy cảm của hàm score $\\psi$ khi hàm phụ $\\eta$ bị dịch chuyển một chút** khỏi giá trị thực $\\eta^$.  
Biểu thức toán học trên slide:\*  
$$\\frac{\\partial}{\\partial r} f(\\eta^\* \+ r(\\eta \- \\eta^\*))$$  
chính là việc chúng ta tạo ra một đường đi tuyến tính giữa hàm phụ ước lượng được và hàm phụ thực tế, sau đó tính tốc độ thay đổi của hệ thống dọc theo đường đi đó."

#### **3\. Khái niệm 2: Tính trực giao Neyman (Neyman Orthogonality)**

\*"Từ đạo hàm Gateaux, chúng ta đi đến định nghĩa quan trọng nhất của DML: **Tính trực giao Neyman** (Định nghĩa A.2).  
Một hàm score được gọi là trực giao Neyman nếu đạo hàm Gateaux của nó **bằng 0 tại điểm của hàm phụ thực tế** (tức là khi $r \= 0$):\*  
$$\\left. \\frac{\\partial}{\\partial r} f(\\eta^\* \+ r(\\eta \- \\eta^\*)) \\right|\_{r=0} \= 0$$

* **Giải thích một cách trực quan:** Các bạn hãy tưởng tượng chúng ta đang đứng ở đáy của một thung lũng parabolic mượt mà. Tại vị trí đáy này (tương ứng với hàm phụ thực tế $\\eta^\*$), nếu bạn có bước lệch sang trái hay sang phải một chút (do mô hình Machine Learning bị sai số), thì độ cao của bạn (tương ứng với giá trị ước lượng causal $\\hat{\\psi}$) **gần như không thay đổi** ở bậc tuyến tính thứ nhất.

Nói cách khác, tính trực giao Neyman giúp triệt tiêu hoàn toàn sai số bậc nhất (first-order bias) do mô hình Machine Learning gây ra. Sai số còn sót lại chỉ là sai số bậc hai (second-order), vốn nhỏ hơn rất nhiều và biến mất rất nhanh khi kích thước mẫu tăng lên."\*

#### **4\. Chốt ý: Tầm quan trọng đối với dữ liệu phụ thuộc (SSI)**

\*"Trong môi trường dữ liệu Shared-State Interference, các quan sát liên kết chặt chẽ với nhau theo chuỗi Markov. Nếu không có tính trực giao Neyman, sai số từ mô hình ML ở bước thời gian này sẽ tích lũy và khuếch đại qua trạng thái chung $H\_t$ sang các bước thời gian tiếp theo, khiến bộ ước lượng cuối cùng bị chệch nghiêm trọng.  
Chính vì vậy, việc chứng minh và thiết kế được một hàm score thỏa mãn tính trực giao Neyman dưới điều kiện dữ liệu SSI là một trong những thành tựu kỹ thuật lớn nhất của các tác giả bài báo này."\*

#### **5\. Chuyển ý (Kết thúc Slide)**

"Bây giờ, khi đã có thuật toán (Slide 9\) và hiểu được cơ chế bảo vệ lý thuyết (Slide 10), chúng ta hãy cùng xem Định lý chính của toàn bộ nghiên cứu sẽ phát biểu như thế nào ở Slide 11 ngay sau đây."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Sử dụng cử chỉ tay hoặc hình ảnh "Cân bằng":** Khi giải thích về tính trực giao (đạo hàm bằng 0), bạn hãy dùng tay mô phỏng một đường cong lòng chảo (parabola) và chỉ vào điểm đáy phẳng để khán giả dễ hình dung khái niệm "độ nhạy bằng 0".  
* **Tránh sa đà vào chứng minh:** Bạn chỉ cần nói công thức này *là gì* và nó mang lại *lợi ích gì* (triệt tiêu sai số bậc nhất). Tuyệt đối không cần giải thích cách tính đạo hàm này ra sao, trừ khi hội đồng phản biện yêu cầu trong phần Q\&A.  
* **Nhấn mạnh từ khóa:** Cụm từ **"Triệt tiêu sai số bậc nhất" (First-order bias cancellation)** là từ khóa "đắt giá" nhất ở slide này, hãy nói chậm và rõ cụm từ này.

# Slide 11

Nội dung này được chia làm 3 phần cốt lõi: **Đặt vấn đề**, **Phát biểu định lý**, và **Ý nghĩa của bộ ước lượng phương sai**.

### **Kịch bản thuyết trình chi tiết cho Slide 11**

#### **1\. Dẫn nhập và Đặt vấn đề (Mở đầu Slide)**

"Thưa các bạn, sau khi đã thiết lập được thuật toán DML cho SSI ở slide trước, câu hỏi quan trọng nhất đặt ra là: **Liệu bộ ước lượng $\\hat{\\psi}$ này có thực sự tốt không, và làm sao để chúng ta làm suy luận thống kê (như tính p-value hay xây dựng khoảng tin cậy) khi dữ liệu không còn độc lập (non-iid)?** Định lý 3.3 chính là câu trả lời cốt lõi và là đóng góp lý thuyết nặng ký nhất của bài báo này."

#### **2\. Phát biểu Định lý chính & Tính chuẩn tắc tiệm cận**

"Định lý 3.3 khẳng định rằng: Dưới các giả định về cấu trúc chuỗi ngẫu nhiên (Assumption 2.1), tính trực giao Neyman (Assumption 3.1) và tốc độ hội tụ của các mô hình Machine Learning phụ trợ (Assumption 3.2), bộ ước lượng DML của chúng ta sẽ đạt được **Tính chuẩn tắc tiệm cận (Asymptotic Normality)**.  
*Cụ thể, công thức toán học trên slide:*  
$$\\sqrt{T}\\sigma^{-1}(\\psi(W\_{1:T}; \\hat{\\eta}) \- \\psi^\*) \\xrightarrow{d} N(0,1)$$  
cho thấy sai số giữa giá trị ước lượng và giá trị thực, khi được chuẩn hóa bằng phương sai $\\sigma$, sẽ hội tụ về phân phối chuẩn chuẩn tắc khi kích thước mẫu $T$ tiến ra vô cùng. Điều này có nghĩa là chúng ta có thể sử dụng các kiểm định giả thuyết thống kê truyền thống một cách an toàn, ngay cả khi các mô hình ML làm nhiệm vụ ước lượng hàm phụ là các mô hình phi tham số vô cùng phức tạp."

#### **3\. Điểm mấu chốt: Bộ ước lượng phương sai nhất quán ($\\hat{\\sigma}^2$)**

"Tuy nhiên, trong thực tế, chúng ta không hề biết phương sai thực $\\sigma^2$. Để xây dựng khoảng tin cậy 95%, bắt buộc ta phải tìm được một **bộ ước lượng phương sai nhất quán** $\\hat{\\sigma}^2$ từ dữ liệu thực tế.  
Đây chính là nơi tính chất phụ thuộc dữ liệu của SSI làm cho bài toán trở nên thách thức. Trong môi trường iid thông thường, bạn chỉ cần dùng công thức cắm (plug-in) lấy phương sai mẫu là xong. Nhưng ở đây, do có sự nhiễu loạn giữa các bước thời gian, các tác giả đã phải tách ra thành 2 trường hợp cụ thể để thiết kế bộ ước lượng phương sai:

* Trường hợp thứ nhất \- Hệ thống thỏa mãn tính chất Hình học Ergod (Geometric Ergodicity): Các bạn có thể thấy công thức toán trên slide sử dụng kỹ thuật chia mẫu thành các block $T\_1$ và $T\_2$. Plug-in variance thông thường sẽ bị chệch trong chuỗi Markov. Vì vậy, phương pháp tính phương sai theo block này giúp triệt tiêu các hiệp phương sai tích lũy theo thời gian, đảm bảo tính nhất quán tiệm cận cho $\\hat{\\sigma}^2$.  
* Trường hợp thứ hai \- Hệ thống có tính phụ thuộc hữu hạn ($m$-dependence): Được ứng dụng trực tiếp cho các thử nghiệm Switchback. Vì các quan sát cách nhau xa hơn $m$ bước hoàn toàn độc lập, chúng ta có thể dùng bộ ước lượng dạng plug-in mở rộng. Công thức này bao gồm một số hạng tính phương sai thông thường, cộng thêm các số hạng hiệp phương sai (covariance) của các đơn vị nằm trong phạm vi $m$ bước liền kề để bù trừ cho phần nhiễu loạn.

#### **4\. Chuyển ý (Kết thúc Slide)**

"Tóm lại, Định lý 3.3 không chỉ chứng minh mặt lý thuyết rằng DML hoạt động tốt dưới sự nhiễu loạn SSI, mà quan trọng hơn, nó cung cấp cho các nhà thực hành một công cụ toán học chính xác để tính toán khoảng tin cậy trong thực tế. Ngay sau đây, chúng ta sẽ xem các tác giả hiện thực hóa định lý này vào hai bài toán cụ thể như thế nào."

### **💡 Mẹo nhỏ cho bạn khi nói slide này:**

* **Tương tác trực quan:** Khi nói đến đoạn *"công thức toán học trên slide"*, hãy dùng con trỏ laser hoặc chuột chỉ vào biểu thức $\\sqrt{T}\\sigma^{-1}(\\dots)$.  
* **Nhấn mạnh từ khóa:** Hãy nhấn mạnh các từ **"Chuẩn tắc tiệm cận"** (Asymptotic Normality) và **"Nhất quán"** (Consistent). Đây là hai thuộc tính "vàng" mà bất kỳ nhà thống kê nào cũng tìm kiếm trong một bộ ước lượng.  
* **Hạ thấp độ phức tạp:** Đừng đi quá sâu vào chứng minh toán học của Gateaux derivative hay Harris ergodic trừ khi có người hỏi ở phần Q\&A. Hãy tập trung vào việc *tại sao* công thức này lại quan trọng (vì nó giải quyết được sự phụ thuộc dữ liệu).

# Slide 12

Dưới đây là kịch bản thuyết trình chi tiết cho **Slide 12: Ứng dụng 1 \- Ước lượng Tác động Trực tiếp Trung bình (Average Direct Effect \- ADE)**.  
Mục tiêu của slide này là đưa những lý thuyết trừu tượng ở các slide trước vào một bài toán thực tế cụ thể: **Dữ liệu quan sát (Observational Data)** dưới sự nhiễu loạn của trạng thái chung.

### **Kịch bản thuyết trình chi tiết cho Slide 12**

#### **1\. Dẫn nhập: Bước vào các ứng dụng thực tế**

"Thưa các bạn, sau khi đã đi qua toàn bộ phần khung lý thuyết và các định lý toán học cốt lõi, phần tiếp theo của bài thuyết trình sẽ là nơi chúng ta nhìn thấy **sức mạnh thực tiễn** của nghiên cứu này. Các tác giả đã hiện thực hóa định lý DML cho SSI vào hai bài toán thực tế lớn. Bài toán đầu tiên, nằm ở Slide 12 này, là ước lượng **Tác động Trực tiếp Trung bình (Average Direct Effect \- ADE)** trong môi trường dữ liệu quan sát."

#### **2\. Định nghĩa mục tiêu ước lượng (The Estimand: ADE)**

"Trước hết, chúng ta cần hiểu **ADE** nghĩa là gì trong ngữ cảnh này? Các bạn có thể nhìn vào công thức định nghĩa trên slide:  
$$\\psi^\* \\triangleq \\frac{1}{T}\\sum\_{t=1}^{T}\\mathbb{E}\_{P}\[Y\_t(1,H\_t) \- Y\_t(0,H\_t)\]$$  
Về mặt trực quan, ADE đo lường mức độ thay đổi kết quả của một cá thể khi chúng ta chuyển trạng thái đối xử của **chính cá thể đó** từ Kiểm soát (0) sang Đối xử (1), trong khi giữ nguyên phân phối đối xử của tất cả những người khác xung quanh.  
Ví dụ thực tế: Trên nền tảng gọi xe công nghệ, ADE trả lời cho câu hỏi: Nếu hệ thống phát mã giảm giá cho riêng tài xế $t$, thì doanh thu của tài xế đó thay đổi ra sao, giả định rằng lượng tài xế xung quanh nhận mã giảm giá vẫn không đổi."

#### **3\. Cấu trúc bộ ước lượng DML điều chỉnh theo Trạng thái chung (The Estimator)**

"Trong dữ liệu quan sát, việc ước lượng ADE cực kỳ thách thức vì có sự xuất hiện của các biến gây nhiễu (confounders). Đặc biệt, trạng thái chung $H\_t$ (ví dụ: lượng xe trống trên bản đồ tại thời điểm đó) vừa ảnh hưởng đến việc tài xế có nhận được cuốc xe hay không ($Y\_t$), vừa liên quan đến việc hệ thống có phân phối mã giảm giá hay không ($D\_t$). Nếu chúng ta bỏ qua $H\_t$, kết quả ước lượng chắc chắn sẽ bị chệch (biased).  
Để giải quyết bài toán này, các tác giả đã thiết kế một bộ ước lượng đặc biệt, chia làm hai thành phần chính như công thức trên slide:

* **Thành phần thứ nhất \- Plug-in Component ($\\varphi^{pi}$):** Đây là hàm hồi quy phi tham số $f(D\_t, X\_t, H\_t)$ dùng để dự đoán kết quả dựa trên các đặc trưng của cá thể và **đặc biệt là có chứa đối số trạng thái chung $H\_t$**. Thành phần này đóng vai trò như một bước điều chỉnh covariate cho trạng thái chung nhằm kiểm soát sự gây nhiễu.  
* **Thành phần thứ hai \- Debiasing Component ($\\varphi^{db}$):** Thành phần này mô phỏng theo cấu trúc AIPW (Augmented Inverse Probability Weighting) truyền thống, sử dụng Propensity Score $m(X\_t)$ (xác suất nhận đối xử dựa trên đặc trưng). Số hạng này đóng vai trò tối quan trọng: nó là **thành phần sửa sai** giúp bộ ước lượng đạt được tính trực giao Neyman mà chúng ta đã thảo luận ở Slide 10, bảo vệ kết quả khỏi các sai số từ mô hình ML ước lượng hàm $f$ và $m$\[\]."\*

#### **4\. Điểm mấu chốt cần lưu ý (The Nuance)**

"Có một điểm rất quan trọng mà tôi muốn các bạn lưu ý ở đây: **Chúng ta không thể đơn thuần coi trạng thái chung $H\_t$ giống như một covariate iid thông thường rồi ném vào mô hình DML tiêu chuẩn**. Tại sao? Bởi vì dữ liệu $H\_t$ phụ thuộc chặt chẽ theo chuỗi thời gian thông qua cấu trúc Markov. Hệ thống của chúng ta là một chuỗi dữ liệu phụ thuộc chuỗi (time-dependent data). Nếu coi chúng là iid, việc ước lượng phương sai và khoảng tin cậy sau đó sẽ hoàn toàn sai lệch, và lát nữa ở phần mô phỏng các bạn sẽ thấy bằng chứng thực nghiệm cho điều này."

#### **5\. Chuyển ý (Kết thúc Slide)**

"Tóm lại, cấu trúc bộ ước lượng tại Slide 12 này đã hiện thực hóa thành công lý thuyết DML vào việc xử lý nhiễu loạn trạng thái chung trong dữ liệu quan sát. Tiếp theo, ở Slide 13, chúng ta sẽ chuyển sang một ứng dụng thậm chí còn phổ biến hơn trong công nghiệp: Thử nghiệm Switchback nhằm ước lượng tác động toàn cục."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Kết nối với thực tế:** Hãy dùng các ví dụ quen thuộc về các nền tảng công nghệ (Grab, Uber, TikTok, Airbnb) khi nói về trạng thái chung (như giá cả, thuật toán gợi ý, hay lượng xe trống). Điều này giúp khán giả hiểu ngay lập tức tại sao bài toán toán học này lại có giá trị kinh tế lớn.  
* **Nhấn mạnh vào đối số $H\_t$:** Khi chỉ vào công thức hàm $f(1, X\_t, H\_t)$, hãy nhấn mạnh từ **"$H\_t$ nằm ở đây"**. Đây là điểm khác biệt cốt lõi so với các mô hình hồi quy thông thường không tính đến interference.  
* **Giữ nhịp độ ổn định:** Do slide này bắt đầu xuất hiện các ký tự toán cụ thể của bộ ước lượng AIPW ($\\varphi^{pi} \+ \\varphi^{db}$), hãy nói chậm lại một chút để người nghe kịp nhìn và liên hệ với khái niệm "Hàm Score trực giao" ở Slide 9 và 10\.

# Slide 13

Dưới đây là kịch bản thuyết trình chi tiết cho **Slide 13: Ứng dụng 2 \- Thử nghiệm Switchback cho Tác động Toàn cục (Global Average Treatment Effect \- GATE)**.  
Slide này chuyển sang một bài toán vô cùng quen thuộc trong môi trường công nghiệp (như tại các công ty công nghệ lớn Uber, Grab, DoorDash): **Thử nghiệm A/B theo thời gian (Switchback Experiments)** để đo lường tổng tác động khi bật/tắt một tính năng trên toàn hệ thống.

### **Kịch bản thuyết trình chi tiết cho Slide 13**

#### **1\. Dẫn nhập: Bước sang ứng dụng quan trọng trong thực tế công nghiệp**

*"Thưa các bạn, ở Slide 12, chúng ta đã xem cách DML xử lý dữ liệu quan sát để tìm tác động trực tiếp lên từng cá thể. Bây giờ, chúng ta sẽ bước sang một ứng dụng thực tế và cực kỳ phổ biến trong môi trường công nghiệp: **Thử nghiệm Switchback (Switchback Experiments)** để ước lượng **Tác động Toàn cục (Global Average Treatment Effect \- GATE)**."*

#### **2\. Định nghĩa Mục tiêu ước lượng: Tác động Toàn cục (GATE)**

*"Trước hết, hãy cùng làm rõ **GATE** là gì và tại sao nó lại quan trọng. Các bạn có thể nhìn vào công thức định nghĩa trên slide:*  
$$\\tau^\* \\triangleq \\mathbb{E}\\left\[ Y\_t(1, \\mathbf{1}) \- Y\_t(0, \\mathbf{0}) \\right\]$$  
\*Trái ngược với ADE ở slide trước (chỉ đổi đối xử của một người), GATE đo lường **sự khác biệt của toàn bộ hệ thống** trong hai viễn cảnh hoàn toàn trái ngược: \*

* *Một là: Tất cả mọi cá thể đều nhận đối xử (Treatment) và hệ thống vận hành ở trạng thái chung khi bật tính năng đó.*  
* *Hai là: Tất cả mọi cá thể đều thuộc nhóm kiểm soát (Control) và hệ thống vận hành ở trạng thái chung khi tắt tính năng.*

*Ví dụ thực tế: Nếu Grab muốn đổi thuật toán định giá tự động mới, họ cần biết: Nếu áp dụng thuật toán này cho **toàn bộ** thành phố (GATE), tổng doanh thu sẽ tăng bao nhiêu so với việc giữ thuật toán cũ cho **toàn bộ** thành phố? Chúng ta không thể chia đôi tài xế trong cùng một khu vực vì họ sẽ cạnh tranh và làm nhiễu kết quả của nhau thông qua trạng thái chung (giá cả thị trường)."*

#### **3\. Cơ chế của Thử nghiệm Switchback truyền thống và Hạn chế**

*"Để giải quyết vấn đề nhiễu luận này, các kỹ sư thường dùng **Thử nghiệm Switchback**: Toàn bộ hệ thống sẽ được bật tính năng mới trong 30 phút, sau đó tắt trong 30 phút tiếp theo, và cứ lặp đi lặp lại như vậy theo chuỗi thời gian.*  
*Tuy nhiên, thách thức ở đây là **sự phụ thuộc hữu hạn theo chuỗi thời gian (m-dependence)**. Trạng thái chung ở khối thời gian này (ví dụ: lượng tài xế đang bận) sẽ kéo dài và ảnh hưởng sang khối thời gian ngay sau đó. Nếu tính toán theo cách thông thường, phương sai của bộ ước lượng sẽ cực kỳ lớn, đồng nghĩa với việc bạn phải chạy thử nghiệm trong nhiều tuần liền thì kết quả mới đạt ý nghĩa thống kê."*

#### **4\. Giải pháp DML cho Switchback: Giảm phương sai vượt trội**

\*"Chính lúc này, bộ ước lượng DML dành cho cấu trúc $m$-dependence phát huy sức mạnh. Như các bạn thấy trên slide, thay vì chỉ so sánh trung bình đơn thuần giữa các khối thời gian, các tác giả đã đưa vào một thành phần gọi là **Regression Adjustment** dựa trên Machine Learning.  
Bộ ước lượng sử dụng mô hình ML để dự đoán kết quả tiềm năng dựa trên các covariates $X\_t$ và trạng thái chung từ quá khứ. Bằng cách 'trừ bớt' đi phần biến động có thể dự đoán được này khỏi kết quả thực tế $Y\_t$, DML4SSI đã **loại bỏ được phần lớn nhiễu ngẫu nhiên** trong chuỗi thời gian.\*  
*Về mặt toán học, bộ ước lượng này vẫn thỏa mãn tính trực giao Neyman và tính chuẩn tắc tiệm cận của Định lý 3.3. Nhưng về mặt thực tiễn, việc đưa ML vào điều chỉnh giúp **giảm đáng kể phương sai** (Variance Reduction) của bộ ước lượng."*

#### **5\. Chốt ý: Ý nghĩa kinh tế của Ứng dụng**

*"Đối với các doanh nghiệp, việc giảm phương sai này mang một ý nghĩa kinh tế vô cùng to lớn: **Nó cho phép bạn rút ngắn thời gian chạy thử nghiệm A/B xuống một nửa hoặc một phần ba** mà vẫn đạt được độ chính xác tương đương. Bạn có thể đưa ra quyết định kinh doanh nhanh hơn, tiết kiệm chi phí vận hành và giảm thiểu rủi ro khi thử nghiệm các tính năng lỗi.*  
*Ngay sau đây, ở phần kết quả thực nghiệm, chúng ta sẽ được nhìn thấy những con số cụ thể chứng minh cho khả năng giảm phương sai ấn tượng này của thuật toán."*

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Minh họa trực quan về Switchback:** Nếu có thể, hãy dùng tay mô phỏng trục thời gian dịch chuyển (ví dụ: Khối 1: Bật \-\> Khối 2: Tắt \-\> Khối 3: Bật) để khán giả dễ hình dung khái niệm Switchback.  
* **Nhấn mạnh sự khác biệt giữa ADE và GATE:** Hãy làm bật lên sự khác biệt: ADE là tác động *vi mô* (micro), còn GATE là tác động *vĩ mô* (macro) lên toàn bộ nền tảng. Khán giả trong ngành cực kỳ quan tâm đến GATE.  
* **Sử dụng từ khóa "Giảm phương sai" (Variance Reduction):** Trong thử nghiệm A/B, giảm được phương sai là "chén thánh". Hãy nhấn mạnh từ khóa này vì nó giải thích lý do tại sao phương pháp toán học phức tạp này lại đáng để áp dụng vào thực tế.

# Slide 14

### **Kịch bản thuyết trình chi tiết cho Slide 14**

#### **1\. Dẫn nhập: Bước vào phần minh chứng bằng con số**

\*"Thưa các bạn, ông bà ta có câu 'Nói có sách, mách có chứng'. Sau khi đi qua một loạt công thức toán học và thiết lập bộ ước lượng cho Tác động Trực tiếp Trung bình (ADE) ở Slide 12, câu hỏi thực tế tiếp theo luôn là: **Mô hình này chạy trên dữ liệu mô phỏng sẽ cho kết quả như thế nào so với các phương pháp truyền thống?**  
Slide 14 này chính là câu trả lời trực quan nhất, dựa trên các biểu đồ thực nghiệm thu được từ Hình 2 và Hình 3 của bài báo."\*

#### **2\. Phân tích Biểu đồ Độ chệch (Hình 2 \- Mật độ phân phối sai số)**

"Đầu tiên, xin mời các bạn nhìn vào biểu đồ mật độ phân phối độ chệch (Bias) ở bên trái slide. Các tác giả đã thực hiện mô phỏng 50,000 lần và so sánh phương pháp của chúng ta — ký hiệu là **DML4SSI** (màu đỏ) — với ba phương pháp ngây thơ khác:

* **Phương pháp Horvitz-Thompson truyền thống (HT \- màu xanh dương):** Hoàn toàn bỏ qua trạng thái chung. Kết quả là phân phối của nó lệch hẳn sang bên phải, bị chệch nghiêm trọng so với vạch 0\.  
  * **Phương pháp Naive DML (DML-N \- màu tím):** Phương pháp này học một mô hình dự đoán kết quả nhưng lại loại bỏ biến trạng thái chung $H\_t$ ra khỏi mô hình. Nó cũng bị chệch rất nặng về phía bên trái.  
  * **Phương pháp Naive Plug-in (màu xanh lá):** Dù có đưa $H\_t$ vào mô hình nhưng lại dùng công thức cắm (plug-in) trực tiếp từ mô hình Machine Learning mà không có thành phần sửa sai (debiasing). Kết quả là nó hội tụ chậm và vẫn bị chệch một khoảng rõ rệt.

Nhìn vào vạch đứt nét màu đen tại vị trí 0 — đại diện cho ước lượng hoàn hảo không bị chệch — các bạn có thể thấy **chỉ duy nhất phân phối của DML4SSI (màu đỏ) là nằm đối xứng và ôm trọn vạch số 0**. Điều này chứng minh bộ ước lượng của bài báo thực sự loại bỏ được định kiến sai số một cách triệt để."

#### **3\. Phân tích Biểu đồ Khoảng tin cậy (Hình 3 \- Độ phủ và Độ rộng)**

"Tiếp theo, hãy nhìn vào hai biểu đồ đường ở phía bên phải, biểu diễn kết quả khi chúng ta tăng dần kích thước mẫu $T$ từ $10^2$ lên $10^4$.

* **Biểu đồ Độ phủ (Coverage):** Đường nét đứt ngang trên cùng chính là mục tiêu lý tưởng: khoảng tin cậy 95% thì phải chứa giá trị thực trong 95% số lần thử nghiệm. Ba phương pháp HT, Plug-in và Naive DML do bị chệch quá nặng nên tỷ lệ phủ của chúng gần như bằng 0, nằm bẹp dí ở đáy biểu đồ.  
  * **Điểm thú vị nhất nằm ở đường màu cam \- Phương pháp SSAC (Shared-State As Covariates):** Đây là phương pháp **coi trạng thái chung giống hệt như một covariate iid thông thường**. Về mặt toán học, bộ ước lượng của nó giống của chúng ta, nên nó không bị chệch. Tuy nhiên, do nó giả định dữ liệu độc lập (iid) và bỏ qua các hiệp phương sai theo chuỗi thời gian của trạng thái chung, **nó đã đánh giá thấp phương sai thực tế**.

Hậu quả là gì? Các bạn nhìn sang biểu đồ **Độ rộng (Width)** ở góc dưới cùng bên phải: Khoảng tin cậy của đường màu cam SSAC bị bóp quá hẹp so với thực tế. Khoảng tin cậy quá hẹp dẫn đến việc độ phủ của nó chỉ loanh quanh ở mức 60% đến 70% và hoàn toàn không thể hội tụ về mức 95% mục tiêu dù kích thước mẫu có tăng lên bao nhiêu đi nữa.  
Trong khi đó, **đường màu đỏ DML4SSI của chúng ta tiến rất mượt mà và tiệm cận chính xác về độ phủ 95%** nhờ vào bộ ước lượng phương sai nhất quán đã tính đến cấu trúc phụ thuộc chuỗi thời gian của SSI."

#### **4\. Chốt ý và Kết luận Slide**

"Kết quả thực nghiệm ở Slide 14 này đưa ra một thông điệp rất rõ ràng: Trong môi trường có sự nhiễu loạn trạng thái chung, việc bỏ qua nhiễu loạn (như HT, DML-N) hay việc xử lý sai bản chất phụ thuộc chuỗi của dữ liệu (như SSAC) đều dẫn đến những sai lầm nghiêm trọng trong suy luận thống kê. DML4SSI là giải pháp toàn diện giải quyết được cả hai vấn đề này."

#### **5\. Chuyển ý (Kết thúc Slide)**

"Đó là kết quả dành cho dữ liệu quan sát và ADE. Bây giờ, chúng ta hãy cùng chuyển sang Slide 15 để xem hiệu năng của thuật toán đối với bài toán thử nghiệm Switchback và tác động toàn cục GATE ra sao."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Nhấn mạnh vào đường màu cam (SSAC):** Đối với các khán giả có chuyên môn về Data Science hay Thống kê, họ thường sẽ có tư duy: *"Tại sao không đưa $H\_t$ vào làm covariate thông thường cho nhanh?"*. Hãy nhấn mạnh phần giải thích về đường màu cam để bẻ gãy tư duy này ngay lập tức. Đây là điểm nhấn học thuật rất mạnh của slide.  
* **Điều chỉnh tông giọng:** Khi nói đến đoạn *"chỉ duy nhất phân phối của DML4SSI là ôm trọn vạch số 0"* hoặc *"tiến rất mượt mà về độ phủ 95%"*, hãy dùng giọng điệu tự hào và khẳng định để tăng tính thuyết phục của phương pháp.  
* **Chỉ dẫn trực quan:** Biểu đồ này có rất nhiều màu sắc khác nhau (đỏ, cam, xanh lá, xanh dương, tím). Bạn nên sử dụng chuột hoặc con trỏ để chỉ rõ từng màu tương ứng với phương pháp nào để khán giả không bị loạn mắt.

# Slide 15

Slide này mang tính chất quyết định để thuyết phục các nhà quản lý hoặc các kỹ sư thực hành trong doanh nghiệp, bởi nó chứng minh khả năng **tiết kiệm tài nguyên và tối ưu hóa chi phí thử nghiệm** (thông qua việc giảm phương sai) của phương pháp DML4SSI.

### **Kịch bản thuyết trình chi tiết cho Slide 15**

#### **1\. Dẫn nhập: Chuyển sang kết quả thực nghiệm của Thử nghiệm Switchback**

\*"Tiếp theo, xin mời các bạn bước sang Slide 15\. Sau khi đã chứng minh được hiệu năng vượt trội của mô hình đối với dữ liệu quan sát, chúng ta sẽ cùng nhìn vào các bằng chứng thực nghiệm dành cho **Thử nghiệm Switchback nhằm ước lượng Tác động Toàn cục (GATE)**.  
Đây là phần kết quả mà các doanh nghiệp công nghệ lớn cực kỳ quan tâm, vì nó đánh giá trực tiếp khả năng tối ưu hóa quy trình thử nghiệm A/B theo chuỗi thời gian của bài báo."\*

#### **2\. Phân tích Biểu đồ so với các phương pháp ngây thơ (Hình 4 \- Độ chệch)**

"Đầu tiên, hãy nhìn vào biểu đồ mật độ phân phối độ chệch ở phía bên trái (Hình 4). Tương tự như bài toán ADE, các tác giả đã chạy mô phỏng 50,000 lần. Các bạn có thể thấy một bức tranh lặp lại:  
\* \* Các phương pháp ngây thơ như **Horvitz-Thompson** (màu xanh dương), **Naive DML** (màu tím) hay **Plug-in** (màu xanh lá) đều lệch rất xa so với vạch đích số 0, tức là chúng bị chệch nghiêm trọng. \* \* **Đặc biệt là đường màu cam \- Phương pháp SSAC (Shared-State As Covariates):** Khi chúng ta xử lý trạng thái chung như một covariate iid thông thường để ước lượng GATE, kết quả bị chệch nặng về phía bên trái. Lý do kinh tế đằng sau rất trực quan: phương pháp này vô tình kiểm soát và triệt tiêu luôn các hiệu ứng lan tỏa (spillover effects) giữa các đơn vị, thay vì gộp chúng vào tổng tác động. Mà bản chất của GATE là phải bao gồm cả tác động trực tiếp lẫn tác động gián tiếp.  
Một lần nữa, **chỉ có phân phối DML4SSI của chúng ta (màu đỏ) là hội tụ chính xác và tập trung ngay tại vạch số 0**, chứng minh tính không chệch của bộ ước lượng."

#### **3\. Điểm nhấn cốt lõi: So sánh với Bộ ước lượng Switchback chuẩn (Hình 5 \- Giảm phương sai)**

"Bây giờ, xin mời các bạn nhìn vào biểu đồ ở giữa slide (Hình 5). Đây chính là **'khoảnh khắc tỏa sáng'** của nghiên cứu này. Các tác giả đã đưa DML4SSI (màu đỏ) lên bàn cân với **bộ ước lượng Switchback Horvitz-Thompson chuẩn (SB \- màu vàng)** được đề xuất bởi Bojinov và các cộng sự năm 2022 — vốn là phương pháp không chệch tiêu chuẩn hiện nay trong công nghiệp.  
*Nhìn vào biểu đồ, các bạn sẽ thấy:* \* \* **Cả hai mô hình đều không chệch:** Cả phân phối màu đỏ và màu vàng đều tâm đầu ý hợp nằm ngay vạch số 0\. \* \* **Nhưng hình dáng của chúng hoàn toàn khác biệt:** Phân phối màu vàng (SB) trải rất rộng và dẹt, nghĩa là phương sai của nó rất lớn. Trong khi đó, phân phối màu đỏ (DML4SSI) cực kỳ nhọn và thu hẹp vào trung tâm, chứng minh **phương sai thấp hơn một cách vượt trội**.  
\* **Tại sao DML4SSI lại giảm được phương sai mạnh mẽ như vậy?** Có hai lý do cốt lõi: Thứ nhất, mô hình đã tận dụng sức mạnh của Machine Learning để học và giải thích các biến động của dữ liệu thông qua đặc trưng cá thể và trạng thái chung. Thứ hai, bộ ước lượng Switchback truyền thống bắt buộc phải vứt bỏ dữ liệu của $m$ bước đầu tiên sau mỗi lần bật/tắt tính năng để tránh nhiễu, còn **DML4SSI thì tận dụng được toàn bộ dữ liệu của chuỗi thời gian mà không cần bỏ sót quan sát nào**."\*

#### **4\. Phân tích kết quả Khoảng tin cậy (Hình 6 \- Tiết kiệm cỡ mẫu)**

"Cuối cùng, hãy nhìn vào biểu đồ Hình 6 ở phía bên phải để thấy hệ quả của việc giảm phương sai này lên khoảng tin cậy: \* \* Về **Độ phủ (Coverage)**: DML4SSI (đường màu đỏ) hội tụ rất chuẩn về mức 95%. Trong khi đó, đường màu vàng (SB) luôn đạt độ phủ tuyệt đối 100%. Lý do không phải vì nó quá tốt, mà vì bộ ước lượng phương sai của nó quá bảo thủ (conservative).\* \* \* Minh chứng là ở biểu đồ **Độ rộng (Width)**: Độ rộng khoảng tin cậy của phương pháp SB truyền thống (màu vàng) **lớn gấp 3 đến 7.5 lần** so với DML4SSI (màu đỏ).\*  
Ý nghĩa thực tiễn ở đây là gì? Để đạt được một khoảng tin cậy có độ hẹp chấp nhận được, phương pháp truyền thống đòi hỏi một lượng dữ liệu khổng lồ với thời gian chạy thử nghiệm kéo dài. Còn với DML4SSI, **bạn cần ít mẫu hơn rất nhiều để đưa ra một kết luận kinh doanh có cùng độ chính xác**."

#### **5\. Chốt ý và Kết luận Slide**

"Tóm lại, Slide 15 khẳng định giá trị thương mại to lớn của nghiên cứu: Không chỉ giải quyết bài toán lý thuyết, DML4SSI là một công cụ giúp các công ty công nghệ tối ưu hóa chi phí, tăng tốc độ thử nghiệm tính năng mới và đưa ra quyết định dựa trên dữ liệu một cách nhanh chóng và chính xác hơn bao giờ hết."

#### **6\. Chuyển ý (Kết thúc Slide)**

"Và để tổng kết lại toàn bộ các luận điểm, đóng góp cũng như mở ra những hướng đi tiếp theo của nghiên cứu này, chúng ta sẽ bước vào phần thảo luận cuối cùng ở Slide 16."

### **💡 Mẹo trình bày Slide này cho bạn:**

* **Nhấn mạnh từ "Ý nghĩa kinh tế" (Economic Impact):** Khi trình bày biểu đồ Hình 5 và Hình 6, hãy đổi góc nhìn từ "nhà toán học" sang "nhà quản lý". Việc giảm phương sai và thu hẹp khoảng tin cậy đồng nghĩa với việc **tiết kiệm tiền và thời gian** cho công ty. Đây là luận điểm thuyết phục nhất đối với người nghe trong môi trường thực tế.  
* **Giải thích trực quan đồ thị nhọn/dẹt:** Dùng con trỏ chuột vẽ theo độ nhọn của đường màu đỏ để khán giả thấy sự tập trung của dữ liệu. Giải thích ngắn gọn: *"Càng nhọn nghĩa là độ đâm trúng mục tiêu càng cao và ít sai số ngẫu nhiên"*.  
* **Chuẩn bị cho câu hỏi Q\&A:** Khán giả rất dễ hỏi câu: *"Tại sao bộ ước lượng cũ (SB) phải bỏ dữ liệu mà bộ ước lượng này lại giữ được?"*. Câu trả lời nằm ở chỗ: DML sử dụng thành phần điều chỉnh hồi quy (Regression Adjustment) từ ML để chủ động 'trừ nhiễu' tích lũy của $m$ bước trước đó, thay vì phải đợi hệ thống tự hết nhiễu theo thời gian một cách bị động.

# Câu hỏi có thể bị hỏi:

1) Về việc slide 9 (apply DML vào SSI): "Tại sao không dùng K-fold Cross-fitting thông thường?" 

→ "Vì trong SSI, $Y\_t$ phụ thuộc vào $H\_{t-1}$. K-fold thông thường sẽ làm xáo trộn thứ tự thời gian và phá vỡ mối quan hệ Markov này, dẫn đến ước lượng sai lệch phương sai." 