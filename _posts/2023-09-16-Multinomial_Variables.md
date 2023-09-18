---
title: 2.1 Multinomial Variables 
tags: [chap2]
math: true
---
## 
### 1.Định nghĩa 

* Trong bài trước chúng ta đã tìm hiểu Binary Variables với biến $x = 0$ hoặc $x = 1$. Đơn giản nó biểu diễn được cho một trạng thái. Nhưng chúng ta có thể gặp những bài toán mà 1 biến thể hiện cho nhiều trạng thái mà vẫn muốn sử dụng giá trị nhị phân thì sao ? 

* Chúng ta sẽ sử dụng vector K-chiều với 1 phần từ bằng 1 và các phần tử khác bằng 0. Ví dụ với $K = 6$: 

$$x = (0,1,0,0,0,0)^T$$

* Từ đó ta có :
$$\sum_{k=1}^Kx_k = 1$$

* Nếu ta đặt $p(x_k = 1) = \mu_k$ ta có công thức likehood: 
$$p(x|\boldsymbol{\mu}) = \prod_{k=1}^K\mu_k^{x_k}$$

trong đó $\boldsymbol{\mu} = (\mu_1,\mu_2,...,\mu_K)^T$ với điều kiện $0 \leq \mu_i$ và $\sum_k\mu_k = 1$

=> Phân phối trên được coi là khái quát hóa của phân phối Bernouli cho nhiều hơn 2 đầu ra.

Có thể thấy phân phối đã tự chuẩn hóa : 
$$\sum_xp(x|\boldsymbol{\mu}) = \sum_{k=1}^K = 1$$
Và  từ đó ta có *mean* và *var*: 

$$\mathbb{E}[x|\boldsymbol{\mu}] = \sum_xp(x|\boldsymbol{\mu}).x= \sum\{0.\mu_1 + 0.\mu_2 + ...1.\mu_k +...\} = \boldsymbol{\mu}$$

$$var[x|\boldsymbol{\mu}] = \sum_i^K(x_i - \mathbb{E}[x])^2.p(x_i)$$

Theo tìm hiểu thì đây là: <b>Categorical Distribution</b>  --> Sẽ ôn tập sau 

### 2.Likelihood function 

$$p(D|\mu) = \prod_{n=1}^N\prod_{k=1}^K\mu_k^{x_{nk}} = \prod_{k=1}^K\mu_k^{(\sum_nx_{nk})} = \prod_{k=1}^K\mu_k^{m_k}$$

trong đó $m_k = \sum_nx_{nk}$ ( số lần trả về $x_k = 1$)

Sau đó ta maximum likelihood bằng cách maximum log-likelihood nhưng kèm với ràng buộc $\sum\mu_k = 1$

Ta có: 

$$\sum_{k=1}^Km_kln(\mu_k) + \lambda(\sum_{k=1}^K\mu_k -1)$$ 

Đạo hàm theo $\mu_k$ và cho = 0 ta được: 

$$\mu_k = \frac{-m_k}{\lambda}$$

mà $\sum\mu_k = 1 \text{ và} \sum m_k = N$ nên $\lambda = -N $ 

vậy:
$$\mu^* = \frac{m_k}{N}$$

Chúng ta cũng xem xét phân phối của biến m nó được gọi là <b>multinomial distribution</b> 
$$ Mult(m_1,m_2,..,m_k|\boldsymbol{\mu},N) = \frac{N!}{m_1!m_2!...m_k!}\prod_{k=1}\mu_k^{m_k}$$

### 3.Dirichlet distribution 
Bên trên chúng ta đã xét Maximum Likelihood (MLE). Bây giờ chúng ta xét đến Maximum A Posterior (MAP). Mà việc đầu tiên cần là chúng ta tìm một phân phối thích hợp làm prior distribution cho multinomial distribution - conjugate. 

Phân phối đó chính là Dirichlet Distribution .

$$Dir(\mu|\alpha) \sim \prod_{k=1}^K\mu_k^{\alpha_k-1}$$

trong đó $\boldsymbol{\alpha}=(\alpha_1,\alpha_2,..,\alpha_K)^T$ là tham số của phân phối và $"\sim"$ chứ không phải "=" vì còn tiền tố $\Gamma(\alpha)$ để normalized

Từ đó ta có posterior distribution: 

$$p(\mu|D,\alpha) \sim p(D|\mu).p(\mu|\alpha) \sim \prod_{k=1}^K\mu_k^{a_k+m_k -1}$$