#include "Eval.h"

extern bool caseSensitive;

ngram_struct Get_ngram(const vector<string>&reference ,const string & cand)
{
	vector<string> ref = reference;
	string candidate = cand;

	ngram_struct res;
	res.ref_length = 1000;
	int j;
	for(j=0; j<(int)ref.size(); j++)
	{
		NormalizeText(ref[j]);
	//	cout << ref[j] << endl;
	}
	NormalizeText(candidate);

	map<string,int> tst_ngram;
	vector<string> tst_wrds;
	split(candidate,tst_wrds);
	Words2Ngrams(tst_wrds,tst_ngram);

	map<string,int>::iterator itx=tst_ngram.begin();
	/*	for(;itx!=tst_ngram.end(); itx++)
	{
	out<<(*itx).first<<" "<<(*itx).second<<endl;
	}
	out<<endl;*/

	for(j=0;j<MAX_NGRAM;j++) // compute ngram counts
		res.tst_count[j]=j<(int)tst_wrds.size()?(int)tst_wrds.size()-j:0;

	map<string,int>ref_ngram_max;
	for(j=0; j<(int)ref.size(); j++)//对一个句子的参考译文
	{
		map<string,int> ref_ngram;
		vector<string> ref_words;
		split(ref[j],ref_words);
		Words2Ngrams(ref_words,ref_ngram);
		//
		/*out<<"ref"<<j<<endl;
		for(itx=ref_ngram.begin();itx!=ref_ngram.end(); itx++)
		{
		out<<(*itx).first<<" "<<(*itx).second<<endl;
		}
		out<<endl;*/
		//
		map<string,int>::iterator it;
		for(it=ref_ngram.begin(); it!=ref_ngram.end();it++)
		{
			string ngram = (*it).first;
			vector<string> wrds;
			if(ref_ngram_max.find(ngram)!=ref_ngram_max.end())
			{
				if(ref_ngram_max[ngram] < ref_ngram[ngram])
					ref_ngram_max[ngram] = ref_ngram[ngram];
			}
			else
				ref_ngram_max[ngram] = ref_ngram[ngram];
		}
		//
		/* out<<"max"<<endl;
		for(itx=ref_ngram_max.begin();itx!=ref_ngram_max.end(); itx++)
		{
		out<<(*itx).first<<" "<<(*itx).second<<endl;
		}
		out<<endl;*/
		//

		if((int)ref_words.size()<res.ref_length)
			res.ref_length=ref_words.size();
	}
	map<string,int>::iterator it2;
	for(it2=tst_ngram.begin(); it2!=tst_ngram.end(); it2++)
	{
		string ngram = (*it2).first;
		if(ref_ngram_max.find(ngram)== ref_ngram_max.end())
			continue;
		vector<string> wrds;
		split(ngram,wrds);

		int mt;
		if(tst_ngram[ngram]>ref_ngram_max[ngram])
			mt = ref_ngram_max[ngram];
		else
			mt = tst_ngram[ngram];
		res.match_cnt[wrds.size()-1] +=mt;
	}
	//
	/*	out<<endl;
	out<<"length "<<res.ref_length<<endl;
	copy(res.match_cnt.begin(),res.match_cnt.end(),ostream_iterator<int>(out," "));
	out<<endl;
	copy(res.tst_count.begin(),res.tst_count.end(),ostream_iterator<int>(out," "));
	out<<endl;*/

	//
	return res;
}

int split(const string&s,vector<string>&words)
{
	istrstream b(s.c_str());
	string t;
	words.clear();
	while(b>>t)
	{
		if(t.size()>0)
			words.push_back(t);
	}
	return words.size();
}
void Words2Ngrams(const vector<string> & words,map<string,int> & count)
{
	int i;
	count.clear();
	for(i=0;i<(int)words.size();i++)
	{
		int j;
		string ngram;
		ngram="";
		for(j=0;j<MAX_NGRAM && i+j<(int)words.size();j++)
		{
			if (j>0)
				ngram+=" ";
			ngram+=words[i+j];
			if (count.find(ngram)!=count.end())
				count[ngram]++;
			else
				count[ngram]=1;
		}
	}
}
void  NormalizeText(string& s)
{
	int i,w;
	string t;

	replace(s,"-\n","");
	replace(s,"\n"," ");
	replace(s,"\t"," ");
	replace(s,"&quot;","\"");
	replace(s,"&amp;","&");
	replace(s,"&lt;","<");
	replace(s,"&gt;",">");

	w=0;
	for(i=0;i<(int)s.length();i++)
	{
		char & c=s[i];
		if (c>='A' && c<='Z' || c>='a' && c<='z' || c>='0' && c<='9')
		{
			if (w==0)
			{
				w=1;
			}
			t+=c;
		}
		else
			if (c>='{' && c<='~' || c>='[' && c<'`' 
				||c>' ' && c<='&' || c>='(' && c<='+'
				||c>=':' && c<='@' || c=='/')
			{
				w=0;
				t+=' ';
				t+=c;
				t+=' ';
			}
			else
				if (c=='.' || c==',')
				{
					if (i>0 && (s[i-1]>='0' && s[i-1]<='9')
						&& i+1<(int)s.length() && (s[i+1]>='0' && s[i+1]<='9'))
					{
						w=0;
						t+=c;
					}
					else
					{
						w=0;
						t+=' ';
						t+=c;
						t+=' ';
					}
				}
				else
					if (i>0 && (s[i-1]>='0' && s[i-1]<='9') && c=='-')
					{
						w=0;
						t+=' ';
						t+=c;
						t+=' ';
					}
					else
						if (c==' ')
						{
							int u,v;
							for(u=i-1;u>=0;u--)
							{
								if (s[u]!=' ')
									break;
							}
							for(v=i+1;v<(int)s.length();v++)
							{
								if (s[v]!=' ')
									break;
							}
							if (u>=0 && v<(int)s.length() && s[u]>='0' && s[u]<='9' && s[v]>='0' && s[v]<='9')
							{
								t+="";
							}
							else
							{
								t+=c;
							}
							w=0;
						}
						else
						{
							w=0;
							t+=c;
						}
	}
	s=t;

	replace(s,"  "," ");
	if (s.length()>0 && s[0]==' ')
		s=s.substr(1);
	if (s.length()>0 && s[s.length()-1]==' ')
		s=s.substr(0,s.length()-1);

	//大小写不敏感
	if(!caseSensitive)
	{
		for(i=0; i<s.size(); i++)
		{
			if(s[i] >='A' && s[i] <='Z')
			{
				s[i] +=32;
			}
		}

	}
	/*for(i=0; i<s.size(); i++)
	{
		if(s[i] >='A' && s[i] <='Z')
		{
			s[i] +=32;
		}
	}*/
}
void replace(string & s,const string t,const string r)
{
	int p;
	p=0;
	while (1)
	{
		p=s.find(t);
		if (p<0)
			return;
		s=s.substr(0,p)+r+s.substr(p+t.length());
	}
}
vector<double> mwer_Levenshtein(string seg, string ref)
{
	vector<string> tstlist,reflist;
	vector<int> mt;
	vector<double> res;
	int i,j;
	int _Y;
	int _X;
	int v;
	//	printf("%s\n%s\n",w2c(seg).c_str(),w2c(ref).c_str());
	split(seg,tstlist);
	split(ref,reflist);

	_Y=tstlist.size();
	_X=reflist.size();
	v=_Y+1;
	mt.resize((_X+1)*v);
	mt[0]=0;
	for(j=0;j<_Y;j++)
		mt[0*v+j+1]=mt[0*v+j]+1; // ins
	for(i=0;i<_X;i++)
	{
		mt[(i+1)*v+0]=mt[i*v+0]+1; // del
		for(j=0;j<_Y;j++)
		{
			int a,b,c;
			a=mt[i*v+j]+(tstlist[j].compare(reflist[i])==0?0:1); // sub
			b=mt[i*v+j+1]+1; // del
			c=mt[(i+1)*v+j]+1; // ins
			mt[(i+1)*v+j+1]=a<b?(a<c?a:c):(b<c?b:c);
		}
	}
	res.resize(3);
	res[0]=mt[_X*v+_Y];
	res[1]=_Y;
	res[2]=_X;
	//	printf("%f %f %f\n",res[0],res[1],res[2]);
	return res;
}