#ifndef EVAL_H
#define EVAL_H

#include <iostream>
#include <string>
#include <strstream>
#include <vector>
#include <map>
#include <fstream>
#include <stdlib.h>
#include <stdio.h>
using namespace std;

const int MAX_NGRAM = 4;

struct ngram_struct
{
	friend ostream & operator<<(ostream &out, const ngram_struct &right)
	{
		for(size_t i=0; i<MAX_NGRAM; i++)
		{
			out << right.match_cnt[i] << " " << right.tst_count[i] << " ";
		}
		out << right.ref_length;
		return out;
	}

	ngram_struct()
	{
		ref_length = 0;
		match_cnt.resize(MAX_NGRAM );
		tst_count.resize(MAX_NGRAM );
	}
	ngram_struct& operator=(const ngram_struct& right)
	{
		ref_length=right.ref_length;
		match_cnt=right.match_cnt;
		tst_count = right.tst_count;
		return (*this);
	}
	ngram_struct& operator+(const ngram_struct &right)
	{
		ref_length += right.ref_length;
		for(size_t i=0; i<MAX_NGRAM; i++)
		{
			match_cnt[i] += right.match_cnt[i];
			tst_count[i] += right.tst_count[i];
		}
		return *this;
	}
	ngram_struct& operator-(const ngram_struct &right)
	{
		ref_length -= right.ref_length;
		for(size_t i=0; i<MAX_NGRAM; i++)
		{
			match_cnt[i] -= right.match_cnt[i];
			tst_count[i] -= right.tst_count[i];
		}
		return *this;
	}

	int ref_length;
	vector<int> match_cnt;
	vector<int> tst_count;
} ;

void Words2Ngrams(const vector<string> & words,map<string,int> & count);//获取ngram信息
int split(const string &s,vector<string>&words);//将句子按空格分割
void replace(string & s,const string t,const string r);
void NormalizeText(string & s);
ngram_struct Get_ngram(const vector<string>&reference,const string & cand);//计算ngram信息

//编辑距离　
vector<double> mwer_Levenshtein(string seg, string ref);


/*void main()
{
	string s1="Please give me a hamburger and the saucepan on the right .";
	string s2 ="Please offer me a hamburger and the saucepan on the right .";
	string s3="I want a hamburger and the saucepan on the right .";
	string s4="Give me a hamburger and saucepan on the right please .";

	vector<string> ref;
	ref.push_back(s1);ref.push_back(s2);ref.push_back(s3);ref.push_back(s4);

	string candidate = "please come a ham and the right the stew .";
	Get_ngram(ref,candidate);


}*/

#endif