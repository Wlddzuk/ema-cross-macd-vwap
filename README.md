EMA Cross Strategy with MACD and VWAP

This PineScript (v6) code combines multiple technical indicators to generate a buy signal when specific conditions are met. It is designed for use on TradingView.

Key Indicators
	1.	Exponential Moving Averages (EMAs)
	•	Fast EMA (default length = 9)
	•	Medium EMA (default length = 20)
	•	Slow EMA (default length = 200)
	2.	Moving Average Convergence Divergence (MACD)
	•	Fast length (default = 12)
	•	Slow length (default = 26)
	•	Signal length (default = 9)
	3.	Volume Weighted Average Price (VWAP)
	•	Calculated with hlc3 (i.e., (high + low + close) / 3).

Buy Signal Logic

A buy signal is generated when all of the following conditions are true:
	1.	EMA Order:
	•	Fast EMA > Medium EMA > Slow EMA
(i.e., 9 EMA > 20 EMA > 200 EMA)
	2.	Price Above VWAP:
	•	Current close > vwap
	3.	MACD Crossover:
	•	The MACD line crosses above the Signal line

When these conditions align, a red arrow labeled “BUY” appears below the bar.

How It Works
	1.	EMA Calculation

ema9 = ta.ema(close, 9)
ema20 = ta.ema(close, 20)
ema200 = ta.ema(close, 200)


	2.	MACD Calculation

[macdLine, signalLine, _] = ta.macd(close, 12, 26, 9)


	3.	VWAP Calculation

vwap = ta.vwap(hlc3)


	4.	Buy Signal Conditions

emaOrderCorrect = ema9 > ema20 and ema20 > ema200
priceAboveVwap = close > vwap
macdCrossover  = ta.crossover(macdLine, signalLine)

buySignal = emaOrderCorrect and priceAboveVwap and macdCrossover



Plots
	•	EMA 9 (white)
	•	EMA 20 (green)
	•	EMA 200 (red)
	•	VWAP (yellow)
	•	MACD (blue)
	•	Signal (orange)

A buy signal is indicated by a red arrow labeled “BUY” below the bar.

Alerts

The script includes an alert condition for when the buy signal is triggered:

alertcondition(buySignal, title="Buy Signal Alert", message="Buy Signal Detected!")

This lets you set up TradingView alerts to be notified whenever a potential buy condition occurs.

How to Use
	1.	Copy the Code:
Save the code above as a .pine file or copy it directly.
	2.	Open TradingView:
Go to TradingView.com and sign in (or create an account if needed).
	3.	Open the Pine Editor:
	•	Click the Pine Editor tab at the bottom of the chart.
	4.	Paste the Script:
	•	Create a new script, paste the code, and save.
	5.	Add to Chart:
	•	Click Add to Chart and the script will apply to your current chart.
	6.	Configure Alerts (optional):
	•	Once the script is on your chart, you can set alerts using the “Buy Signal Alert” condition to get notifications.

Customization
	•	Adjust the EMA lengths, MACD settings, and any other parameters from the Settings menu after you add the script to your chart.
	•	The default lengths are good starting points, but feel free to experiment based on your time frame and trading style.

Disclaimer

This script is for educational purposes only and does not constitute financial advice. Always perform your own research and consider using additional tools before placing any trades. Past performance does not guarantee future results.
