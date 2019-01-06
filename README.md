# Significance_BLEU_Score
<br />
Evaluate the BLEU score significance statistically compare Ref file and Tgt file in machine translation
<br /><br />
----------------------------------------------ENGLISH VERSION-----------------------------------------------------

<br />
[1] Function Describtion: test whether the results of two translation systems are significant
  
<br />
[2] Command-line arguments: SignTestBleu -c -s source.sgm -r reference.sgm -t testoutput.sgm -b baseline.sgm
  
<br />
[3] Data formats: Same as the format of NIST. This program outputs three files "good.xml"， "bad.xml" and "equal.xml" that represent the sentences in "testoutput.smg" perform better , worse and same quality as the sentences in "baseline.sgm" (Note that the translation quality is evaluated with BELU score)
  
<br />
[4] Calculation Details:
      
<br />
  Comparing the different translation results in two files: testoutput.sgm and baseline.sgm , for example, if sentences s1 s2 and s3 are different, we initially replace the s1 s2 s3 sentences in baseline.sgm by using the counterpart sentences in testout.smg. then calculate the BLEU scores for the baseline file , if the aforementioned replacement enables the BLEU score to increase, we make the f(+)+=1, if the BLEU score decreases, then let f(-)+=1 , or if there is no change after replacing, then let f(0)+=1.
      
<br />
  How to calculate the value of Z: Z = |(n-N/2)/sqrt(N/4)|， here n= f(+)， N = f(+) + f(-)
      
<br />
  z>1.96, significance 95%， z>2.57, significance 99%

  
<br />
----------------------------------------------CHINESE VERSION-----------------------------------------------------
  
<br />
[1] 本程序功能： 测试两个翻译系统的结果是不是显著的
  
<br />
[2] 命令行参数： SignTestBleu -c -s source.sgm -r reference.sgm -t testoutput.sgm -b baseline.sgm
  
<br />
[3] 格式：同NIST评测的格式。程序输出3个文件，good.xml， bad.xml, equal.xml分别代表testoutput.smg比baseline.sgm好的句子，坏的句子，和bleu值相等的句子
  
<br />
[4] 说明：  
<br />
  比较testoutput.sgm 和 baseline.sgm的不同翻译结果，例如：s1,s2,s3不同。用testoutput.smg中的s1，s2,s3分别替换baseline中的s1,s2,s3，计算bleu值，如果替换后有助于提高bleu值，则f(+) += 1, 如果降低了bleu值，则f(-) += 1, 否则 f(0) += 1。
   
<br />
  计算z 值： Z = |(n-N/2)/sqrt(N/4)|， 其中n= f(+)， N = f(+) + f(-)
  
<br />
  z>1.96, 显著性95%， z>2.57, 显著性99%

