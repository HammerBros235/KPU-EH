# 전략 1

## 1.  전략 개념

- 순익률이 1020%까지 도달하였으나, 오버피팅이라는 의심의 끈을 놓을 수 없다.
- 모든 종목에서 동일하게 높게 나오는 전략을 찾는 것이 중요하다고 생각.
- 그러나 1/n^m의 확률로 번져 계산적으로 찾기 매우 힘들어짐.

## 2. 전략 구현

- 전략 구현 플랫폼: TradingView
- 전략 코드
    
    ```python
    //@version=2
    strategy("rsi", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100)
    
    rsi = rsi(close, 14)
    rsi_ma = rma(rsi, 28)
    
    longstop = strategy.position_avg_price * (1 - 0.1)
    longprofit = strategy.position_avg_price * (1 + 0.4)
    
    if rsi_ma < 55 and rsi < 30
        strategy.entry("long", strategy.long)
    
    if rsi_ma > 45 and rsi > 70
        strategy.exit("long", stop = longstop, limit = longprofit)
    
    plot(close)
    plot(rsi)
    ```
    

### A. caps

1516.2% w/ H.Potter’s RSI

![Untitled (13)](https://user-images.githubusercontent.com/84055441/217017610-d8d7f8d2-ada6-4dbc-8cd4-2300ed0237df.png)

Possible overfitting - trashed

![Untitled (12)](https://user-images.githubusercontent.com/84055441/217017587-529c398c-aa78-4070-b1fd-c0f3393c4e13.png)

Possible overfitting - trashed

![Untitled (11)](https://user-images.githubusercontent.com/84055441/217017546-23ab17bf-d58a-4dc7-871b-43bdccf38a85.png)

---
