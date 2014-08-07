# node-stanford-corenlp

A simple node.js wrapper for Stanford CoreNLP.

#### What is Stanford CoreNLP?
Stanford CoreNLP provides a set of natural language analysis tools which can take raw English language text input and give the base forms of words, their parts of speech, whether they are names of companies, people, etc., normalize dates, times, and numeric quantities, and mark up the structure of sentences in terms of phrases and word dependencies, and indicate which noun phrases refer to the same entities. Stanford CoreNLP is an integrated framework, which make it very easy to apply a bunch of language analysis tools to a piece of text. Starting from plain text, you can run all the tools on it with just two lines of code. Its analyses provide the foundational building blocks for higher-level and domain-specific text understanding applications.

Stanford CoreNLP integrates all our NLP tools, including the part-of-speech (POS) tagger, the named entity recognizer (NER), the parser, and the coreference resolution system, and provides model files for analysis of English. The goal of this project is to enable people to quickly and painlessly get complete linguistic annotations of natural language texts. It is designed to be highly flexible and extensible. With a single option you can change which tools should be enabled and which should be disabled.

The Stanford CoreNLP code is written in Java and licensed under the GNU General Public License (v2 or later). Source is included. Note that this is the full GPL, which allows many free uses, but not its use in distributed proprietary software. The download is 214 MB and requires Java 1.6+.


## Installation

node-stanford-simple-nlp depends on [Stanford CoreNLP](http://nlp.stanford.edu/software/corenlp.shtml) v3.4. And don't forget to [set proper environment variables](https://github.com/nearinfinity/node-java) like `JAVA_HOME` in your system.

    $ npm install stanford-corenlp

**Important!** You should download `stanford-corenlp-full-2014-06-16.zip` file and unzip to a folder and provide the path in the configuration. You can download the file from [here](http://nlp.stanford.edu/software/stanford-corenlp-full-2014-06-16.zip).


## Configuration
```javascript
var NLP = require('stanford-corenlp');
var config = {"nlpPath":"./corenlp","version":"3.4"};
var coreNLP = new NLP.StanfordNLP(config);
```

## Usage

#### Async mode
```javascript
var NLP = require('stanford-corenlp');

var coreNLP = new NLP.StanfordNLP({"nlpPath":"./corenlp","version":"3.4"},function(err) {
  coreNLP.process('This is so good.', function(err, result) {
    console.log(err,JSON.stringify(result));
  });
});
```

#### Sync mode
```javascript
var NLP = require('stanford-corenlp');

var coreNLP = new NLP.StanfordNLP({"nlpPath":"./corenlp","version":"3.4"});
coreNLP.loadPipelineSync();
coreNLP.process('This is so good.', function(err, result) {
  console.log(err,JSON.stringify(result));
});
```

**Warning!** If you didn't initialize the class without callback function then you will meet `'Load a pipeline first.'` error. So you have to do it with callback function or call `loadPipeline(options, callback)` function seperately.

## 中文
从[这个页面](http://nlp.stanford.edu/software/corenlp.shtml#History)上下载对应的中文包[stanford-chinese-corenlp-2014-02-24-models.jar](http://nlp.stanford.edu/software/stanford-chinese-corenlp-2014-02-24-models.jar)，并下载[StanfordCoreNLP-chinese.properties](https://github.com/stanfordnlp/CoreNLP/raw/master/src/edu/stanford/nlp/pipeline/StanfordCoreNLP-chinese.properties)，放到固定目录中，并在初始化时用`language`参数说明上述两个文件的位置

```javascript
var NLP = require('stanford-corenlp');

var coreNLP = new NLP.StanfordNLP({
  "nlpPath": "./corenlp",
  "version": "3.4",
  language: {
    jar: './corenlp/stanford-chinese-corenlp-2014-02-24-models.jar',
    properties: './corenlp/StanfordCoreNLP-chinese.properties'
  }
}, function (err) {
  coreNLP.process('驼峰摘要是首个提供中文摘要的开放API服务。', function (err, result) {
    console.log(err, JSON.stringify(result));
  });
});
```

## License
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

This license also applies to the included Stanford CoreNLP files.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

Author: Hitesh Joshi (me@hiteshjoshi.com). Copyright 2013~2014.
