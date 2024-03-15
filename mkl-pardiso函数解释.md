



```c++
void pardiso (_MKL_DSS_HANDLE_t pt, const MKL_INT *maxfct, const MKL_INT *mnum, const MKL_INT *mtype, const MKL_INT *phase, const MKL_INT *n, const void *a, const MKL_INT *ia, const MKL_INT *ja, MKL_INT *perm, const MKL_INT *nrhs, MKL_INT *iparm, const MKL_INT *msglvl, void *b, void *x, MKL_INT *error);
```

* pt :输入参数；大小为64的数组，第一次调用pardiso前需要置0。调用pardiso后，不要直接修改pt，可能导致内存泄漏。

    使用pardiso_handle_store or pardiso_handle_store_64将pt内容存储到文件中。使用pardiso_handle_restore or pardiso_handle_restore_64从文件中恢复pt的内容。

* maxfct :输入参数；相同稀疏结构因子的最大数量。（Maximum number of factors with identical sparsity structure）必须保存在内存中。在大多数程序中为1。

* mnum :解空间的实际矩阵，取值为1到maxfct之间，大多数程序中为1。

* mtype :输入参数；用于定义矩阵类型。

     1·实数结构对称矩阵 2·实数对称正定矩阵 -2·实数对称不正定矩阵 3·复数结构对称矩阵 4·复数Hermitian正定矩阵     -4·复数Hermitian不定矩阵 6·复数对称矩阵 11·实数非对称矩阵 13·复数非对称矩阵

* phase :输入参数；用于控制求解器的执行。通常是两位数或三位数，第一个数表示执行的开始阶段，第二个数表示执行的结束阶段。

    1·Fill-reduction analysis and symbolic factorization  填充xx分析和符号分解； 2·数值分解  3·向前和向后求解，包括可选的细化迭代。

    11·分析 12·分析、数值分解 13·分析、数值分解、求解、迭代细化 22·数值分解 23·数值分解、求解、迭代细化 33·求解、迭代细化 331·同33，但是正向取代 332·同33，但是对角替换 333·同33，但是反向取代 0·为L和U矩阵释放内存 -1·释放所有矩阵的内存

    对于阶段332，即涉及到对角替换部分，允许提供自定义实现（如LAPACK ）。

* n :输入参数；方程A*X=b的稀疏线性系统中的方程约束条件。 n>0;

* a :输入参数；数组Array,包括稀疏矩阵A中对应ja的索引的非0元素。系数矩阵可以是实数也可以是复数，但必须以行压缩方式（CSR3）的三数组变体或块行压缩方式（BSR3）的三数组变体存储，矩阵必须以每行递增的ja值存储。data?

    对于CSR3格式，a=ja；对于BSR3格式，a=0；

    注：如果将iparm的值设置为负值，则会将CSR3转为BSR格式（参考espares数据存储）。

* ia:输入参数；数组Array，大小为n+1。对于CSR3格式，ia[i]指向数组ja中第i行的第一个非0元素的列索引。IndexPointer？

* ja:输入参数；数组Array，大小为n。包含稀疏矩阵a的列索引，索引按每行递增的顺序排列。Indices?

* perm :数组；大小为n，根据iparm[4]和iparm[30]的值，保存为大小为n的排列向量，用于计算部分解的元素，或用于低秩更新的输入矩阵的不同值。

    具体看[pardiso (intel.com)](https://www.intel.com/content/www/us/en/docs/onemkl/developer-reference-c/2023-0/pardiso.html#GUID-431916D5-B76D-48A1-ABB5-1A0613FDC0FA)

    注意：iparm[4]=1可防止求解时并行。

* nrhs :需要解的右边的个数。

* iparm :数组Array，大小为64。用于向pardiso传递各种参数，控制位，并在求解器执行后返回一些有用信息。（详见iparm parameters）

* msglvl :输入参数；消息信息。

    0·pardiso不生成输出。 1·输出打印到屏幕上。

* b :输出参数；数组Array，大小n*nrhs。包含right-hand side vector/matrix B，旨在解决方案阶段（solution ）被访问。

    （(See also [Intel MKL PARDISO Parameters in Tabular Form](https://www.intel.com/content/www/us/en/docs/onemkl/developer-reference-c/2023-0/onemkl-pardiso-parameters-in-tabular-form.html#GUID-E1E2E435-241F-47CB-83D5-9322CA21473E)）

* x :输出参数，大小n*nrhs。iparm[5]=0时，它包含解向量/矩阵X。
* error :输出参数，提示出错信息。

原文地址：[pardiso (intel.com)](https://www.intel.com/content/www/us/en/docs/onemkl/developer-reference-c/2023-0/pardiso.html#GUID-431916D5-B76D-48A1-ABB5-1A0613FDC0FA)
