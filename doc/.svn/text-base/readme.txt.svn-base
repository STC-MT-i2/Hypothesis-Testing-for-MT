作者：何中军 zjhe@ict.ac.cn 2008-01-09

[1] 本程序功能： 测试两个翻译系统的结果是不是显著的

[2] 命令行参数： SignTestBleu -c -s source.sgm -r reference.sgm -t testoutput.sgm -b baseline.sgm

[3] 格式：同NIST评测的格式。程序输出3个文件，good.xml， bad.xml, equal.xml分别代表testoutput.smg比baseline.sgm好的句子，坏的句子，和bleu值相等的句子

[4] 说明：
    比较testoutput.sgm 和 baseline.sgm的不同翻译结果，例如：s1,s2,s3不同。用testoutput.smg中的s1，s2,s3分别替换baseline中的s1,s2,s3，计算bleu值，如果替换后有助于提高bleu值，则f(+) += 1, 如果降低了bleu值，则f(-) += 1, 否则 f(0) += 1。
 
   计算z 值： Z = |(n-N/2)/sqrt(N/4)|， 其中n= f(+)， N = f(+) + f(-)

   z>1.96, 显著性95%， z>2.57, 显著性99%