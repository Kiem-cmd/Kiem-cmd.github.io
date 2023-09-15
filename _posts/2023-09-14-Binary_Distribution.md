---
title: 2.1 Binary Distribution 
tags: [chap2]
math: true
--- 


### 1. Bernouli Distribution 

* Chúng ta sẽ xem sét single binary random variable  $x \in \{0,1\}$. Ở đây $x $ có thể là sự kiện khi tung mặt coin, với $x = 1$ thì là "heads" và $x=0$ là "tails"

* Giả sử đồng xu không đồng chất và xác suất để $x = 1$ là $\mu$ (chứ ko phải 0.5) 
Ta có : 

$$p(x=1|\mu) = \mu$$    


và:

$$p(x=0|\mu) = 1- \mu$$

=> Phân phối xác suất của x có thể vướt dưới dạng:

$$Bern(x|\mu) = \mu^x(1-\mu)^{1-x}$$ 

=> đây được gọi là <strong> Bernouli distribution </strong>

* Có thể dễ dàng tính được *mean* và *var* của phân phối xác suất này:

$$\mathbb{E}[x] = \sum x.p(x) = \sum0.p(x=0) + 1.p(x=1) = \mu$$

$$var[x] = \sum (x_i - \mathbb{E}[x])^2*p(x_i) = (0-\mu)^2 * (1-\mu) + (1 -\mu)^2*\mu = \mu(1-\mu)$$

* Bây giờ giả sử chúng ta có tập dữ liệu $D = \{x_1,x_2,..,x_N\}$ với giả thuyết từng $x_i$ là độc lập và giống nhau ta có hàm likelihood như sau: 

$$p(D|\mu) = \prod_{n=1}^{N}p(x_n|\mu)= \prod_{n=1}^N\mu^{x_n}(1-\mu)^{1-x_n}$$

=> Để tối ưu hóa hàm này (Maximum Likelihood) ta tính log 2 vế (Log-Likelihood)

$$Lnp(D|\mu) = \sum_{n=1}^NLnp(x_n|\mu) = \sum_{n=1}^N\{x_nLn(\mu) + (1-x_n)Ln(1-\mu)\}$$

=> Sau đó đạo hàm theo $\mu$ và cho 0 ta được kết quả:

$$\mu^* =\frac{1}{N}\sum_{n=1}^Nx_n = \frac{m}{N}$$ 

trong đó m là số lần tung được "heads"

>Bây giờ giả sử chúng ta tung đồng xu 3 lần và cả 3 lần đầu là "heads". Vậy thì $\mu^* = 1$ ??? Thật không hợp lý -> Maximum Likelihood gây ra ovefitting. Chúng ta sẽ sớm xem làm thể nào để đạt được kết quả tốt hơn, tránh overfitting với <b>prior distribution</b> trên $\mu$ 

### 2. Biomial Distribution 

* Chúng ta sẽ xem xét tham số $m$ (số lần tung đồng xu được "heads"). Đây được là Binomial Distribution( Phân phối nhị thức) 
$$Bin(m|N,\mu) = C^m_N\mu^m(1-\mu)^{N-m}$$

* Có thể coi phân phối nhị thức như nhiều lần phân phối bernouli độc lập với nhau. 
Ta có thể tính được *mean* và *var* của phân phối nhị thức như sau: 

$$\mathbb{E}[m] = \sum_{m=0}^Nm.Bin(m|N\mu) = N\mu $$

$$var[m] = \sum_{m=0}^N(m-\mathbb{E}[m])^2.Bin(m|N,\mu)=N.\mu(1-\mu)$$


![Alt text](/assets/image/image.png)
_Đây là histogram của binomial distribution với N = 10 và $\mu = 0.25$_

### 3. Beta distribution 

* Như chúng ta đã biết việc sử dụng Maximum lkelihood gây ra vấn đề overfitting. Vì thế chúng ta sử dụng 1 phương pháp đã là sử dụng công thức Bayes và hàm cần tối ưu lúc này là <b>Posterior distribution</b>

* Ta có công thức Bayes như sau: 

$$posterior = \frac{likelihood * prior}{evident} <=> p(\mu|x) =  \frac{p(x|\mu) * p(\mu)}{p(x)}$$

* Chúng ta đã có công thức của $likelihood$ rồi, điều cần thiết là bây giờ cần tìm phân phối phù hợp cho $prior$ vì $evident = p(x) $ không liên quan đến $\mu$ 

* Và phân phối mà chúng ta lựa chọn đó là Beta Distribution. Lí do bởi vì đó là *Conjugacy* (liên hợp) của Bernouli distribution. *Conjugacy* của $p(a)$ là $p(b)$ sao cho $p(a) * p(b) ~ p(a)$. Nghĩa là nếu chọn $prior$ là beta distribution thì $posterior$ sẽ có cùng dạng với likehood từ đó dễ maximum hơn.

* Hàm xác suất của beta distribution: 

$$Beta(\mu|\beta) = \frac{1}{\beta}\mu^{a-1}(1-\mu)^{b-1}$$

>trong đó $1/\beta$ là để chuẩn hóa còn a và b là các hyperparameter do chúng ta chọn dựa vào dữ liệu ban đầu.

![Alt text](/assets//image/image-1.png)
_Một vài hình ảnh của beta distribution_

* *Mean* và *Var* của beta distribution : 
$$\mathbb{E}[\mu] = \frac{a}{a+b}$$

$$var[\mu] = \frac{ab}{(a+b)^2(a+b+1)}$$

Từ công thức Bayes ta có : 

$$p(\mu|m,l,a,b)\text{ } \alpha\text{ } Bin(m,l|\mu).Beta(\mu|a,b)\text{ } \alpha\text{ } \mu^{m+ a -1}(1-\mu)^{l+b-1}$$

* Giải thích đơn giản về a và b là sự hiệu quả của số quan sát $x = 1$ và $x = 0$ 
* Với mỗi dữ liệu mới thì a và b sẽ được update 
* Ghi $N - > \infty$ variance (phương sai - sự không chắc chắn) giảm và mean -> $\mu^*$


---------------------
---------------------

Còn một phần nữa nhưng đọc chưa hiểu nên tạm bỏ qua 
..... 