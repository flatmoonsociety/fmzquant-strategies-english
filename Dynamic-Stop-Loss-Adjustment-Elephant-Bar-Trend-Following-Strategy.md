
> Name

Dynamic-Stop-Loss-Adjustment-Elephant-Bar-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/2b69354ead2324cb3cab7ea2ab851c0acbf73ad75ace72094adefc249c591b44.png)

[trans]
#### Overview
This strategy is a trend following system based on bar pattern recognition, which mainly captures potential trend starting points by identifying "elephant bars" in the market (that is, price bars that are significantly larger than the average size). The core feature of the strategy is to adopt a dynamically adjusted stop-loss plan and adaptively adjust the stop-loss position according to the progress of price movement, which not only protects vested profits but also gives the price enough room for fluctuations.
#### Strategy Principle
The operation of the strategy is based on the following key steps:
1. Calculate the average size of the bars in the past specific period as the base value
2. Identify whether the current column meets the characteristics of "elephant column":
   - Cylinder size significantly exceeds the average (configurable multiple)
   - The closing price is within a specific percentage range of the high and low points
   - Or consistent with hammer/inverted hammer morphological characteristics
3. Determine the trading direction according to the direction of the elephant pillar
4. Set initial stop loss and profit targets
5. As the price develops in a favorable direction, dynamically adjust the stop loss position:
   - Move stop loss above cost line when 60% target is reached
   - Further tighten stop loss when 80% target is reached
   - Significantly tighten stop loss and adjust profit target when 90% target is reached
#### Strategic Advantages
1. Dynamic risk management: By dynamically adjusting the stop loss position, the strategy can protect profits while giving the trend room to fully develop.
2. Flexibility of pattern recognition: In addition to the traditional elephant column, it also includes the recognition of special patterns such as hammer lines.
3. Strong parameter adjustability: key parameters such as column size multiples, target percentages, etc. can be flexibly adjusted according to market characteristics.
4. Reasonable risk-return ratio: The initial stop loss is relatively conservative, but it can be dynamically adjusted as the trend develops to obtain greater returns.
#### Strategy Risk
1. Risk of false breakthroughs: False breakthroughs may occur in the elephant bar pattern, and filtering conditions need to be set appropriately.
2. Risk of volatile market: Stop loss may be triggered frequently in a volatile market.
3. Risk of stop loss adjustment: Too aggressive stop loss adjustment may lead to early exit
4. Parameter sensitivity: The strategy effect is more sensitive to parameter settings and needs to be fully tested.
#### Strategy optimization direction
1. Add market environment filtering:
   - Add trend indicators to identify current market environment
   - Adopt different parameter settings in different market environments
2. Improve the stop loss mechanism:
   -Introduction of trailing stop loss
   - Dynamically adjust stop loss distance based on volatility
3. Optimize entry timing:
   - Combined with volume indicators
   - Added reversal confirmation signal
4. Improve profit methods:
   - Achieve partial profit exit
   - Dynamically adjust profit targets based on market structure
#### Summary
This strategy achieves effective tracking of trends by identifying key price patterns in the market and employing dynamic risk management methods. The core advantage of the strategy lies in its adaptive stop-loss management mechanism, which can fully seize trend opportunities while protecting profits. By further optimizing the market environment identification and risk management mechanism, the strategy is expected to achieve stable performance in different market environments.
|| 

#### Overview
This strategy is a trend following system based on bar pattern recognition, primarily identifying "elephant bars" (price bars significantly larger than average) to capture potential trend initiation points. The strategy's key feature is its dynamic stop-loss adjustment scheme, which adaptively modifies stop-loss positions based on price movement progress, both protecting profits and allowing sufficient price flexibility.

#### Strategy Principles
The strategy operates based on the following key steps:
1. Calculate the average bar size over a specific period as a benchmark
2. Identify if the current bar meets "elephant bar" characteristics:
   - Bar size significantly exceeds average (configurable multiplier)
   - Closing price within specific percentage range of high/low
   - Or matches hammer/inverted hammer patterns
3. Determine trade direction based on elephant bar direction
4. Set initial stop-loss and profit targets
5. Dynamically adjust stop-loss as price moves favorably:
   - Move stop-loss above cost when reaching 60% target
   - Further tighten stop-loss at 80% target
   - Significantly tighten stop-loss and adjust profit target at 90% target

#### Strategy Advantages
1. Dynamic risk management: Protects profits while allowing trends to develop through dynamic stop-loss adjustment
2. Pattern recognition flexibility: Includes special patterns like hammer lines beyond traditional elephant bars
3. Strong parameter adaptability: Key parameters like bar size multiplier and target percentages can be adjusted to market characteristics
4. Reasonable risk-reward ratio: Conservative initial stop-loss with dynamic adjustment for larger gains as trends develop

#### Strategy Risks
1. False breakout risk: Elephant bar patterns may produce false breakouts requiring proper filtering conditions
2. Ranging market risk: Frequent stop-losses may be triggered in sideways markets
3. Stop adjustment risk: Aggressive stop-loss adjustments may lead to premature exits
4. Parameter sensitivity: Strategy effectiveness is sensitive to parameter settings, requiring thorough testing

#### Optimization Directions
1. Enhanced market environment filtering:
   - Add trend indicators to identify current market conditions
   - Apply different parameter settings in different market environments
2. Improved stop-loss mechanism:
   - Incorporate trailing stops
   - Dynamically adjust stop distances based on volatility
3. Optimized entry timing:
   - Integrate volume indicators
   - Add reversal confirmation signals
4. Enhanced profit-taking approach:
   - Implement partial profit exits
   - Dynamically adjust profit targets based on market structure

#### Summary
The strategy effectively tracks trends through key price pattern identification and dynamic risk management. Its core advantage lies in the adaptive stop-loss management mechanism, which protects profits while maximizing trend opportunities. Further optimization of market environment recognition and risk management mechanisms shows promise for consistent performance across different market conditions.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-17 00:00:00
end: 2025-01-16 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//@version=6
strategy("Estratégia Barra Elefante com Stop Dinâmico", overlay=true)

// Parâmetros configuráveis
num_barras = input.int(15, title="Número de Barras para Média", minval=1, maxval=100)
percentual_fechamento_valido = input.float(10, title="Percentual do Máximo de Pavio (%)", minval=1, maxval=100)
percentual_condicao_tamanho = input.float(1.8, title="Multiplicador do Tamanho Médio da Barra", minval=0.1, step=0.1)
percentual_lucro = input.float(1.8, title="% de Lucro do Alvo ref. Tam. da Barra", minval=0.1, step=0.1)

var bool executou_entrada = false

// Calcula o tamanho de cada barra
barra_tamanho = math.abs(close - open)

// Calcula a média do tamanho das últimas 'num_barras' barras
media_tamanho = ta.sma(barra_tamanho, num_barras)

// Definição das variáveis para o corpo do candle, sombra superior e sombra inferior
corpo = barra_tamanho
sombra_superior = high - math.max(close, open)
sombra_inferior = math.min(close, open) - low

// Condições para verificar se a sombra é pelo menos 2x maior que o corpo
sombra_sup_maior = sombra_superior >= 2 * corpo
sombra_inf_maior = sombra_inferior >= 2 * corpo

// Define a relação mínima entre a sombra e o corpo
relacao_minima = 2.0

fechamento_valido = ((close >= high - (percentual_fechamento_valido / 100) * (high - low)) or (close <= low + (percentual_fechamento_valido / 100) * (high - low)))

// Condição para verificar se o fechamento está próximo da máxima ou mínima
fechamento_proximo_max = close >= (high - (high - low) * 0.1)  // Fechamento nos 20% superiores
fechamento_proximo_min = close <= (low + (high - low) * 0.1)   // Fechamento nos 20% inferiores

// definição de candle martelo
eh_martelo = (sombra_sup_maior and fechamento_proximo_max) and (math.abs(high - low) > 1.5*media_tamanho)
eh_martelo_invertido = (sombra_inf_maior and fechamento_proximo_min) and (math.abs(low - high) > 1.5*media_tamanho)

// Compara o tamanho da barra atual com a média usando o percentual configurável
condicao_tamanho = (barra_tamanho > percentual_condicao_tamanho * media_tamanho) and (fechamento_valido or (eh_martelo or eh_martelo_invertido))

// Variáveis para entrada
comprar_condicao = (condicao_tamanho and close > open)
vender_condicao = (condicao_tamanho and close < open)

// Stop Loss inicial
stop_loss_compra = low[1] + (barra_tamanho / 5)  // Para compra, stop é na mínima do candle anterior ajustado
stop_loss_venda = high[1] - (barra_tamanho / 5) // Para venda, stop é na máxima do candle anterior ajustado

// Take Profit inicial (multiplicador configurado)
take_profit_compra = close + percentual_lucro * barra_tamanho
take_profit_venda = close - percentual_lucro * barra_tamanho

// Variáveis para controle do progresso do preço
lucro_alvo_60 = close + 0.6 * (take_profit_compra - close)  // 60% do alvo
lucro_alvo_80 = close + 0.8 * (take_profit_compra - close)  // 80% do alvo
lucro_alvo_90 = close + 0.9 * (take_profit_compra - close)  // 90% do alvo

// Ajustes dinâmicos do Stop Loss e Alvo
if (strategy.position_size > 0)  // Para compras
    if (high >= lucro_alvo_60)
        stop_loss_compra := close + 0.1 * barra_tamanho  // Ajusta Stop para 10% acima da entrada
    if (high >= lucro_alvo_80)
        stop_loss_compra := close + 0.5 * barra_tamanho  // Ajusta Stop para 50% acima da entrada
    if (high >= lucro_alvo_90)
        stop_loss_compra := close + 0.8 * barra_tamanho  // Ajusta Stop para 80% acima da entrada
        take_profit_compra := close + 0.5 * barra_tamanho  // Ajusta Alvo para +50% do último fechamento

if (strategy.position_size < 0)  // Para vendas
    if (low <= lucro_alvo_60)
        stop_loss_venda := close - 0.1 * barra_tamanho  // Ajusta Stop para 10% abaixo da entrada
    if (low <= lucro_alvo_80)
        stop_loss_venda := close - 0.5 * barra_tamanho  // Ajusta Stop para 50% abaixo da entrada
    if (low <= lucro_alvo_90)
        stop_loss_venda := close - 0.8 * barra_tamanho  // Ajusta Stop para 80% abaixo da entrada
        take_profit_venda := close - 0.5 * barra_tamanho  // Ajusta Alvo para -50% do último fechamento

// Executando as ordens de compra e venda
if (not executou_entrada) and (comprar_condicao)
    strategy.entry("Compra", strategy.long)
    strategy.exit("Stop Compra", "Compra", stop=stop_loss_compra, limit=take_profit_compra)
    executou_entrada := true  // Marca que a entrada foi feita

if (not executou_entrada) and (vender_condicao)
    strategy.entry("Venda", strategy.short)
    strategy.exit("Stop Venda", "Venda", stop=stop_loss_venda, limit=take_profit_venda)
    executou_entrada := true  // Marca que a entrada foi feita

// Para visualização, vamos colorir as barras
barcolor(comprar_condicao ? color.rgb(14, 255, 22) : na)
barcolor(vender_condicao ? #d606ff : na)
bgcolor((eh_martelo) ? color.new(color.green, 60) : na)
bgcolor((eh_martelo_invertido) ? color.new(color.red, 60) : na)

// Reseta o controle de execução no início de cada nova barra
if barstate.isnew
    executou_entrada := false
```

> Detail

https://www.fmz.com/strategy/478740

> Last Modified

2025-01-17 16:24:18
