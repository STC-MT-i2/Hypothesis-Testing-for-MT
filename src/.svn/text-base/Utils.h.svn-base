// $Id: Utils.h 2007-06-27 hezhongjun $

#ifndef UTILS_H
#define UTILS_H

#include "Eval.h"

#include <vector>
#include <string>
#include <fstream>
#include <math.h>
using namespace std;


bool ReadReference(const string &fname, vector<vector<string> > &ref, int sentNO);

int ReadSentence(const string &fname, vector<string> &trans);

double BLEU(const ngram_struct &n_gram);

void Print (ostream &out, const string &source, const vector<string> &ref,
					 const string &base, const string &sys );
#endif