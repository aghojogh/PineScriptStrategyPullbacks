# Red Candle Base Trading Strategy

A sophisticated Pine Script trading strategy for TradingView that uses complex mathematical calculations to identify high-probability resistance and support levels based on a manually selected red candle.

## 🎯 Overview

This strategy builds multiple resistance levels through a series of calculations, creating a "ladder" of price zones that incorporate historical context, market momentum, and selling pressure. It trades both directions (SHORT and LONG) with a 1:1 risk-reward ratio.

## 📊 Key Features

### Manual Candle Selection
- **Time-based selection**: Choose your base red candle by specifying exact date and time
- **Visual validation**: Confirms if selected candle is red
- **Flexible input**: Year, Month, Day, Hour, Minute inputs for precise control

### Six Calculated Lines
1. **Line 1** (Blue): Low of base red candle - foundation level
2. **Line 2** (Yellow): Midpoint between Line 1 and Line 3 - activity sensor
3. **Line 3** (Red): Initial resistance based on previous candle analysis
4. **Line 4** (Orange): Momentum-adjusted resistance using candle activity
5. **Line 5** (Purple): Major resistance zone (2x amplified)
6. **Line 6** (White): Ultimate trigger level incorporating selling pressure

### Trading Logic

#### Primary Trade: SELL Signal
- **Trigger**: Price touches Line 6
- **Direction**: SHORT
- **Stop Loss**: Entry + (Line 3 - Line 1)
- **Take Profit**: Entry - (Line 3 - Line 1)

#### Recovery Trade: BUY Signal
- **Condition**: Only activates if SELL trade hits stop loss
- **Trigger**: Price touches Line 6 again
- **Direction**: LONG
- **Stop Loss**: Entry - (Line 3 - Line 1)
- **Take Profit**: Entry + (Line 3 - Line 1)

### Risk Management
- **Risk:Reward Ratio**: 1:1 (balanced approach)
- **Breakeven Win Rate**: 50%
- **Maximum Trades**: 2 per setup (one SELL attempt, one BUY recovery if needed)

## 🔬 Calculation Methodology

### Line 3 Calculation (Three Scenarios)
Analyzes the candle **before** the base red candle:
- **If previous candle is RED**: Line 3 = Base low + (2 × base red length)
- **If previous candle is GREEN with high > base red high**: Line 3 = Base low + (2 × distance from base low to green high)
- **If previous candle is GREEN with high ≤ base red high**: Line 3 = Base low + (2 × base red length)

### Sum Calculation (Market Momentum)
Tracks three candles after base red candle that interact with Line 2:
- **Scenario 1**: All 3 touch Line 2 → Sum = Length₁ + Length₂ + Length₃
- **Scenario 2**: Only Candle_1 touches → Sum = Length₁ + Length₂
- **Scenario 3**: Candle_1 & Candle_3 touch → Sum = Length₁ + Length₂ + Length₃
- **Scenario 4**: Candle_1 & Candle_2 touch → Sum = Length₁ + Length₂

### Sum_1 Calculation (Selling Pressure)
Accumulates evidence from all candles after base red candle:
- **If candle crosses Line 4**: Add partial length (Line 4 - candle low)
- **If candle touches Line 4 from below**: Add full candle length

### Final Calculations
- **Line 4** = Line 3 + Sum
- **Line 5** = Line 1 + (2 × distance from Line 1 to Line 4)
- **Line 6** = Line 5 + Sum_1

## 🎨 Customization Options

- **Display Controls**: Show/hide lines, labels, calculation table
- **Color Customization**: Customize each line's color
- **Line Extension**: Adjust how far lines extend to the right
- **Visual Elements**: Toggle labels and information table

## 📈 Use Cases

- **Resistance Trading**: Identify high-probability selling zones
- **Mean Reversion**: Trade bounces from calculated support/resistance
- **Multi-Timeframe Analysis**: Apply to any timeframe for different perspectives
- **Risk Management**: Built-in 1:1 R:R ensures balanced risk exposure

## 🚀 Getting Started

1. Copy the Pine Script code
2. Open TradingView and create a new Pine Script indicator/strategy
3. Paste the code
4. Set your desired base red candle using date/time inputs
5. Observe the calculated lines on your chart
6. Strategy trades automatically when conditions are met

## 📋 Requirements

- TradingView account
- Pine Script v5 compatible
- Basic understanding of support/resistance concepts

## ⚙️ Strategy Parameters

- **Base Red Candle Selection**: Year, Month, Day, Hour, Minute
- **Display Options**: Lines, Labels, Calculation Table
- **Visual Settings**: Line colors, extension length
- **Risk Management**: Automatic 1:1 R:R ratio

## 🧮 Strategic Philosophy

This strategy is based on the principle that **complex mathematical calculations incorporating multiple market factors** create more reliable support and resistance zones than simple technical indicators. By analyzing:
- Historical price context (previous candle)
- Market activity around key levels (Line 2 interactions)
- Actual selling pressure attempts (Line 4 interactions)
- Mathematical amplification (doubling and stacking)

The strategy identifies zones where market psychology and mathematics align for high-probability reversal points.

## ⚠️ Disclaimer

This strategy is for educational and research purposes. Past performance does not guarantee future results. Always practice proper risk management and never risk more than you can afford to lose. Test thoroughly on historical data and paper trade before using real capital.

## 📝 Version

- **Pine Script Version**: v5
- **Strategy Version**: 1.0
- **Last Updated**: January 2026

## 🤝 Contributing

Feel free to fork this project, submit issues, or create pull requests with improvements.

## 📄 License

MIT License - Feel free to use and modify for your own trading research.

---

## 🔗 Related Resources

- [TradingView Pine Script Documentation](https://www.tradingview.com/pine-script-docs/)
- [Pine Script Reference Manual](https://www.tradingview.com/pine-script-reference/v5/)

---

**Note**: This is a complex algorithmic strategy that requires understanding of both technical analysis and Pine Script programming. Recommended for intermediate to advanced traders.
