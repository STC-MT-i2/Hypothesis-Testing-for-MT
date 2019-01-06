#include "Utils.h"


bool ReadReference(const string &fname, vector<vector<string> >  &ref, int sentNO)
{
	ifstream in(fname.c_str());

	string line;	
	vector<string> temp;

	while(getline(in,line))
	{
		if(line.find("<DOC") != string::npos)
		{
			string trans;
			int sn = 0;
			while(getline(in,trans))
			{
				if(trans.find("<seg") != string::npos)
				{
					int pos = trans.find_first_of(">");
					trans.erase(0,pos+1);
					pos = trans.find_last_of("<");
					trans.erase(pos, trans.size()-pos);
			
					ref[sn++].push_back(trans);
				}
				if(sn == sentNO)
					break;
			/*	else if(trans.find("</DOC>") != string::npos)
				{
					if(sn != sentNO)
					{
						cout << "read reference error! sent number= " << sn 
							 << " != source number " << sentNO << endl;
						return false;
					}
					break;
				}*/
			}
		}
	}
	return true;

/*	while (getline(in,line))
	{
		while (getline(in,line))
		{
			if (line.size() > 1)
			{
				temp.push_back(line);
			}
			else
			{
				ref.push_back(temp);
				temp.clear();
				break;
			}
		}
	}
	ref.push_back(temp);*/

}

int ReadSentence(const string &fname, vector<string> &sents)
{
	ifstream in(fname.c_str());

	string line;
	int total=0;

	while(getline(in,line))
	{
		if(line.find("<seg") != string::npos)
		{
			int pos = line.find_first_of(">");
			line.erase(0,pos+1);
			pos = line.find_last_of("<");
			line.erase(pos, line.size()-pos);
			sents.push_back(line);
			total++;
		}
	}
	return total;
}

double BLEU(const ngram_struct &n_gram)
{
	double precision = 0.0;

	for(int i=0; i<MAX_NGRAM; i++)
	{
		precision += log((double)n_gram.match_cnt[i]/(double)n_gram.tst_count[i]);
	}

	precision /= (double)n_gram.match_cnt.size();

	double lratio = n_gram.ref_length / (double)n_gram.tst_count[0];
	double bp = 1.0;
	if(lratio > 1.0)
		bp = exp(1.0-lratio);
	double bleu = bp * exp(precision);
	return bleu;
}

void Print(ostream &out, const string &source, const vector<string> &ref,
					 const string &base, const string &sys )
{
	out << "<src> " << source << " </src>" << endl;
	for(size_t j=0; j<ref.size(); j++)
	{
		out << "<ref id=\"" << j+1 << "\"> " << ref[j] << " </ref>" << endl;
	}
	out << "<base> " << base << " </base>" << endl;
	out << "<sys> " << sys << " </sys>" << endl;
	
}