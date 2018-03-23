# 48. Template Generator

Date: 2018-03-19

## Status

Proposed

## Context

As a house rent agency platform, we need make their contracts from doc/docx to dynamic html template.

Currently, we use ueditor and variable excel for this, we need 1-2 hours for each contract, even with an experienced people.

Ideas:

1. Doc/docx to html;
2. Html can be edit online;
3. Store as templates, support spring, django, what ever.

### Use local scripts

1. [https://github.com/bradmontgomery/word2html][1]
	Only support docx, result not well. Not support doc.
2. [https://github.com/mwilliamson/python-mammoth][2]
	Same as word2html, but not based on Pandoc.

### Use web services

1. [https://www.zamzar.com][3]
	Very good, 100 free each month
2. [https://www.online-convert.com][4]
	Not Good, but better than local
3. [https://convertio.co/zh/document-converter/][5]
	Very good, 6.99$ per month.

## Decision

Pass

## Consequences

Refs: 

* [https://alternativeto.net/software/ckeditor/][6]

[1]:	https://github.com/bradmontgomery/word2html
[2]:	https://github.com/mwilliamson/python-mammoth
[3]:	https://www.zamzar.com
[4]:	https://www.online-convert.com
[5]:	https://convertio.co/zh/document-converter/
[6]:	https://alternativeto.net/software/ckeditor/