# LynxLogix signal desk — three versions

Status: paper only. Human gate required. No live order in this repo.

Venues in scope: Coinbase Advanced Trade preview, Kraken query. Wallets in scope as watch addresses only: Phantom, Kraken Wallet.

Signal sources: TradingView webhook JSON, or CryptoHopper signal payload (exchange, market, type=buy|sell).

## Shared stop rules

- Missing symbol, side, or size: reject.
- Daily loss cap or open-order cap hit: reject.
- Key missing trade permission or holding withdraw/transfer: refuse to load.
- No human approval token: no preview call.
- Phantom and Kraken Wallet never receive a signing request from this desk.

## Design A — Relay

One bot. TradingView alert hits the desk. Schema check. You approve. Coinbase orders/preview or Kraken ticker quote. Audit row. Stop.

## Design B — Ensemble

Ten roles, one queue: Scanner, Regime, Signal, Risk, Sizer, Router, Execution, Exit, Treasury, Audit. Treasury never holds a withdraw key.

## Design C — Mirror

CryptoHopper remains the exchange client. Lynx mirrors the proposal into the gate. Cold wallets are displayed and never signed.
