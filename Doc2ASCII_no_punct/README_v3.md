
[<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/banner.png" width="888" alt="Visit QuantNet">](http://quantlet.de/)

## [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **Doc2ASCII_no_punct** [<img src="https://github.com/QuantLet/Styleguide-and-FAQ/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/)

```yaml

Name of Quantlet : Doc2ASCII_no_punct

Published in : Bachelor Thesis "Probabilistic Topic Models in Natural Language Processing"

Description : Removes all punctuation marks and transforms the input to ASCII

Keywords : text mining, preprocessing, bash, preprocessing, ASCII

Author : Jerome Bau

Submitted : November 17 2016 by Jerome Bau

Input : 'txt file, not contained in this folder because of two reasons (1) size ~ 30GB (2)
copyright protected'

```


### SHELL Code:
```shell
#!/bin/bash
# Transform documents into ASCII and remove all punctuation marks
# Tested on Ubuntu 16.04
declare -a documents=("example1" "example2" "example3")

for i in "${documents[@]}"
do
   	iconv -f ISO-8859-1 -t ASCII//TRANSLIT "$i" > "$i.txt"
	cat "$i.txt" | tr -d '[:punct:]' > "${i}c.txt"
done

```
