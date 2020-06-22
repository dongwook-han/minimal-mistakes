---
layout: post
title: "[번역]GitHub / Advanced Git / 저자 정보 변경하기"
description: ""
category: "Git"
tags: [git, github, filter-branch]
---
{% include JB/setup %}

이 문서는 [Changing author info](https://help.github.com/articles/changing-author-info)의 비공식 번역글이며 GitHub에서 보증, 유지 또는 감독하지 않습니다. 공식 도움글을 보시려면 [help.github.com](https://help.github.com)을 방문하세요.

---

## 저자 정보 변경하기

저장소 히스토리에 저자 정보를 변경할 필요가 있다면 이 스크립트를 사용하여 수행할 수 있습니다.

<div class="alert"><strong>경고 : </strong>이 행동은 저장소 히스토리를 파괴합니다. 경우에 한하여 복제한 저장소에서 하는 것이 좋은 방법입니다. 또한 다른 사람과 공유하고 있는 저장소에 작업하지 마세요. 사용시 자신에게 책임이 있습니다.</div>

	#!/bin/sh
	 
	git filter-branch --env-filter '
	 
	an="$GIT_AUTHOR_NAME"
	am="$GIT_AUTHOR_EMAIL"
	cn="$GIT_COMMITTER_NAME"
	cm="$GIT_COMMITTER_EMAIL"
	 
	if [ "$GIT_COMMITTER_EMAIL" = "your@email.to.match" ]
	then
	    cn="Your New Committer Name"
	    cm="Your New Committer Email"
	fi
	if [ "$GIT_AUTHOR_EMAIL" = "your@email.to.match" ]
	then
	    an="Your New Author Name"
	    am="Your New Author Email"
	fi
	 
	export GIT_AUTHOR_NAME="$an"
	export GIT_AUTHOR_EMAIL="$am"
	export GIT_COMMITTER_NAME="$cn"
	export GIT_COMMITTER_EMAIL="$cm"
	'