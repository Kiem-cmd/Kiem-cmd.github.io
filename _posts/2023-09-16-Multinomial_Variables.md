


## 

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

$$var[x|\boldsymbol{\mu}] = $$
