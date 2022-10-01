---
title: "Python을 이용하여 Telegram 메세지 보내기" 
excerpt: "Python을 이용하여 Telegram bot으로 메세지를 보내는 방법에 대한 설명입니다."
show_date: true
read_time: true

toc: true
toc_sticky: true
toc_label: "Page Index"

header:
  show_overlay_excerpt: true
  overlay_filter: 0.5
  overlay_color: "#FF8D33"

categories: 

- coding
  tags: 
- python
- telegram
- bot
- send message

---

Python을 이용하여 Telegram bot으로 메세지를 보내는 방법을 설명합니다.

# 1. Telegram bot 만들기

1. 먼저 Telegram을 실행하여 상단 돋보기 모양을 클릭한 후 `BotFather`를 검색합니다.

2. `시작`을 클릭한 후 `/newbot`을 입력하여 메세지를 보냅니다.

3. 생성된 Bot의 이름을 물어보는데 적절히 원하는 이름을 입력합니다. 여기서는 `test_message`라고 정하겠습니다.

4. Bot의 Username을 물어보는데 마찬가지로 적절히 원하는 이름을 입력합니다. 단, Username은 반드시 `_bot`으로 끝나야 하며, 기존에 만들어진 이름과 중복되어서는 안됩니다. 여기서는 `test_message_bot`이라고 정하겠습니다. 

5. Bot을 만들고 나면 나오는 메세지에 `t.me/test_message_bot`이라는 링크가 생성되는데 이를 클릭하면 해당 Bot이 있는 방으로 입장할 수 있습니다. 방에 입장하기 전에 링크의 중간쯤에 있는 `HTTP API token`을 미리 복사해둡니다.

6. 방에 입장하고 난 후 아무 메세지나 입력합니다.  그리고나서 아래의 링크에 아까 복사해둔 API token을 합쳐서 브라우저의 주소창에 입력합니다. 이후 나오는 메세지 중 `id`라고 적힌 부분 이후의 숫자로 된 부분을 복사해둡니다.

```
https://api.telegram.org/bot{토큰 값이 들어가는 부분}/getUpdates
```

# 2. Python에서 코드 작성하기

1. 코드를 작성하기 전에 커맨드창을 열어서 telegram 관련 라이브러리인 `python-telegram-bot`를 먼저 설치합니다.
   
   ```
   pip install python-telegram-bot
   ```

2. 테스트를 위해 아래와 같이 간단하게 코드를 입력한 후 실행합니다. 여기에 `ID`와 `API token`은 앞서 복사해둔 값을 사용합니다.

```python
import telegram as tg

chat_id = ID
bot = tg.Bot(token="API token")

bot.sendMessage(chat_id=chat_id, text="Hello World!")
```

3. 상기 코드를 실행하면 Telegram bot 대화창에 `Hello World!`라는 메세지가 뜹니다. 이를 응용하여 보다 다양한 방식의 메세지를 보낼 수 있습니다.
