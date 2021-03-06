## Text-generator

Text-generator program based on the Markov chains

### Summary of theory 

We can synthesize text using symbols, symbol combinations, words, word combinations, sentences.
One of the types of synthesis is frequency synthesis. 

Algorithm of frequency synthesis at the symbol level:

```
string S = empty word
while we haven't reached a string of a given length
  from table of symbols choose symbol C with probability P(C)
  add the symbol C to the string S
```

The result is a string of a given length, consisting of characters .

The resulting string is most likely completely meaningless (and hard to read). You can increase readability by composing a text from the k-combinations most often found in the language. 

To get more readable text, you need to form the text either from words or from combinations of words.

#### Example, based on **Markov chains**:

The algorithm will use a special table of prefixes consisting of two words and suffixes representing one word as initial data. This table is generated by parsing a large text file.

The algorithm generates output phrases by randomly choosing the next suffix for a specific prefix

Algorithm:

```
put first two wirds into W1 and W2
enter W1 and W2
cycle:
  randomly choose W3 from the set of suffixes
  to the prefix W1 and W2
  change W1 and W2 to W2 and W3
  repeat cycle
```

### Parameters
```c++
typedef deque<string> prefix;          // prefix queue 
map<prefix, vector<string> > statetab; // prefix-suffixes
```

```c++
const int NPREF=2; // number of words in prefix
const int MAXGEN=1000; //amount of the output text
```

#### The process of the program:

- open input file tor ead
- the file is read by words and a table of prefixes and suffixes is created in memory 
- after processing the input file, the process of generating the output text begins 
- the first prefix is taken from the table and a continuation is randomly selected for it (suffix) 
- take the next prefix and select the suffix for it again 
- generation ends either when the specified size is reached, or when the last prefix is processed 

### Example

Example of text generation based on the ''Hamlet'', Shekspear

```
That can I; At least, the whisper goes so. 
Our last king, Whose image even but now appear'd to us, Was, 
as you know, by Fortinbras of Norway, Thereto prick'd on by a most emulate pride, 
Dared to the combat; in which our valiant Hamlet-- For so this side of 
```