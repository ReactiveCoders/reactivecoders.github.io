---
layout: post
date:   2015-08-09 13:00:00
categories: linux
---
* will be replace by toc
{:toc}

# Getting started
===================

~~~ bash
script_name=`basename $0 .sh`
# -z = length of string is 0
[ -z "$var" ] && var="initial value"

# regex, then after ;
if [[ "abc" == [abc]* ]]; then
    echo "it is true"
fi

~~~
