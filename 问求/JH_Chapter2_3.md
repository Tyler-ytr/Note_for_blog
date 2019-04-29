# Fundamentals of algorithms
## 2.3.1
- 定义:
  - alphabet:任何非空的有限集合
  - symbol:某个alphabet里面的元素
    - e.g.: $\sum_{bool}=\{0,1\}$
    - $ \sum_{lat}=\{a,b,...z\} $
  - word: 在某个alphabet里面的有限个symbol的序列
  - empty word $\lambda$: 唯一的包含zero symnol的word;
  - $\sum ^*$: 包含所有的alphabet $\sum$ 的word构成的集合
    - for $\sum =\{a,b\},\sum^*=\{\lambda,a,b,aa,ab,ba,bb,aaa,.....\}$
  - length of a word w: 记作|w|,表示w里面的symbols数量
  - $\#_{a}(w)$:a在w里面出现的次数
  - $\sum ^n$=$\{x\in \sum^*|~|x|=n\}$
    - e.g. $\{a,b\}^{3}=\{aaa,aab,aba,baa,abb,bab,bba,bbb\}$
  - $\sum ^+=sum ^*-\{\lambda \}$
  - vw($v\cdot w$):v和w的连结,v和w是两个word;
  - prefix of word w: w=vu中的v;其中u是$\sum$上的某些word
  - suffix of word w: w=xu中的u;
  - subword of word w: w=uzv中的z;
  - language: Every set $L\subseteq \sum ^*$ is called a language over $\sum$;L^C=$\sum ^*-L$(L的补集)
    - $L_1L_2=L_1\circ L_2=\{uv\in (\sum_1 \cup \sum_2)^*|u\in L_1~ and ~v \in L_2\}$
      - $\{a^nb^{2n}|n\in\mathbb{N}\},\{a,b\}$是$\{a,b\}$中的languages
  - 定义$\sum ^*$上面的canonical ordering:
    - 假设$\sum=\{s_1,...s_m\},m\geq 1$,并且让$s_1<s_2...<s_m$,那么对于u,v$\in \sum^*$,
    ![avatar][JH1]
## 2.3.2








[JH1]:data:image/png;base64,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
    