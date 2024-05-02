# 소켓 통신 API
본 문서에서는 메신저봇 R에서 존재하는 프로젝트 타입인 `외부 소켓 통신`으로 송수신 되는 데이터의 구조를 설명합니다.

## 데이터 포맷
가장 범용적으로 많이 쓰이는 json데이터를 stringify한 데이터를 송수신합니다.

json 구조는 기본적으로 다음과 같습니다.

```json
{
    "packetId": "<UUID>",
    "method": "<METHOD>",
    "body": {},
}
```

이떄, 응답은 비교적 간단합니다.

```json
{
    "packetId": "<UUID (SAME)>",
    "method": "<METHOD (SAME)>",
    "body": {
        "status": 0
    },
}
```

## 메신저봇의 역할
기본적으로 메신저봇은 서버 역할로서 포트가 열립니다.

## 메시지 수신
메시지 수신이 감지되면 메신저봇은 다음과 같은 데이터를 연결된 클라이언트에 전송합니다.

```json
{
    "author": {
        "name": "<AUTHOR NAME>",
        "avatar": "<BASE64 ENCODED AVATOR>",
        "userHash": "<AUTHOR HASH>"
    },
    "channel": {
        "name": "<CHANNEL NAME>",
        "id": "<CHANNEL ID>",
        "isDebugRoom": "<IS DEBUG ROOM>",
        "isGroupChat": "<IS GROUP CHAT>",
    },
    "logId": "<CHAT LOG ID>",
    "isMention": "<IS MENTION>",
    "content": "<MSG CONTENT>",
    "packageName": "<NOTIFICATION PACKAGE NAME>",
}
```
> method: receive

## 메시지 송신
클라이언트는 서버로 다음과 같은 요청을 날릴 수 있습니다.

```json
{
    "room": "<ROOM ID OR ROOM NAME>",
    "message": "<MESSAGE>"
}
```
> method: send