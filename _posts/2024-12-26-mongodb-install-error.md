---
layout: single
title: "M1 맥북 MongoDB 설치에러 해결 - MongoNetworkError"
categories: "Javascript"
tags: ["Database", "MongoDB"]

toc: true
toc_sticky: true
---

## 처음 시도한 방법
M1 맥북에 MongoDB를 설치할 때는 [공식문서](https://www.mongodb.com/ko-kr/docs/manual/tutorial/install-mongodb-on-os-x/)를 따라 mongodb-community@8.0 버전으로 설치했다. 설치는 잘 되었지만 실행을 위해 `mongosh`를 입력하면 아래와 같은 MongoNetworkError가 발생했다.
<br/>
```bash
$ mongosh

Current Mongosh Log ID: 676bfdd6ff9028d80dc98a5a
Connecting to:      mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.3.7
MongoNetworkError: connect ECONNREFUSED 127.0.0.1:27017\
```

<br/>
`brew servies list`로 현재 연결상태를 확인했을 때도 `error 4`가 발생했다.
<br/>
```bash
$ brew services list

Name              Status   User File
mongodb-community error  4 root \~/Library/LaunchAgents/homebrew.mxcl.mongodb-community.plist
```

## 원인
아무리 구글링해도 'error 4'가 왜 발생하는지 이유를 찾을 수 없었다. MongoNetworkError 관련해서 모든 블로그의 나오는 방법을 시도해봤지만 같은 에러가 반복 발생했다. 

## 문제 해결
결국 Claude가 문제를 해결해주었다. 먼저 실행중인 mongoDB 프로세를 모두 중단하고 삭제한 뒤 `arm64버전`으로 설치했다. arm은 iOS기기에 주로 사용되는 아키텍처로 비교적 최신 기기에는 arm64가 사용된다고 한다.

<br>
```bash
arch -arm64 brew tap mongodb/brew
```

mongodb-community는 최신버전이 아닌 `6.0버전`으로 설치했다. 이 버전이 Apple Sillicon과 호환성이 더 좋다고 한다.
<br/>
```bash
arch -arm64 brew install mongodb-community@6.0
```
<br/>
MongoDB를 연결한 뒤 `mongosh`로 실행한다.
<br/>
```bash
brew services start mongodb-community@6.0
mongosh
```
<br/>
정상적으로 실행이 되었다면 커서 모양이 바뀌어야 한다.
