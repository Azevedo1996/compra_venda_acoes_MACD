!pip install yfinance
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import yfinance as yf
%matplotlib inline
     
# Selecionando a ação que queremos trabalhar
ticker = 'ITUB4.SA'
acao = yf.Ticker(ticker)
df = acao.history(period='1y')
df = df[['Close']]
     
# Ajustando o formato da data
df.index = pd.to_datetime(df.index).strftime('%Y-%m-%d')
     
# Calculando a Média Móvel Exponencial (EMA) de 12 e 26 dias
ema_12 = df.ewm(span=12, adjust=False).mean()
ema_26 = df.ewm(span=26, adjust=False).mean()
     
# Calculando o Moving Average Convergence Divergence (MACD)
macd = ema_12 - ema_26
     
# Calculando a linha de sinal como a EMA de 9 dias do MACD
signal_line = macd.ewm(span=9, adjust=False).mean()
     
# Plotando o gráfico com o preço, MACD e linha de sinal
plt.figure(figsize=(12,8))
plt.plot(df, label='Preço')
plt.plot(macd, label='MACD', color='red')
plt.plot(signal_line, label='Linha de Sinal', color='green')
plt.legend(loc='upper left')
plt.title(f'Análise MACD para {ticker}')
plt.show()

# Sinal de Compra e Venda
last_macd = macd[-1]
last_signal_line = signal_line[-1]

if last_macd > last_signal_line:
    print(f"Sinal de compra para {ticker}")
elif last_macd < last_signal_line:
    print(f"Sinal de venda para {ticker}")
else:
    print(f"Sinal neutro para {ticker}")
