# Crypto-analytics
-- Daily Transaction Volume for SOL token
SELECT
  DATE(t.block_time) AS date,
  COUNT(*) AS total_transactions,
  SUM(t.fee) AS total_volume
FROM solana.transactions AS t
WHERE
  t.success = TRUE
GROUP BY
  DATE(t.block_time)
ORDER BY
  date;

  -- Top 10 Wallets by SOL Holdings
SELECT 
    to_wallet AS wallet_address,
    SUM(amount) AS sol_holdings
FROM 
    solana_transactions
WHERE 
    token_symbol = 'SOL'
GROUP BY 
    to_wallet
ORDER BY 
    sol_holdings DESC
LIMIT 10;

-- Token Distribution among Wallets
SELECT 
    token_symbol,
    COUNT(DISTINCT to_wallet) AS unique_wallets
FROM 
    solana_transactions
GROUP BY 
    token_symbol
ORDER BY 
    unique_wallets DESC
LIMIT 10;

-- Average Transaction Size per Token
SELECT 
    token_symbol,
    AVG(amount) AS avg_transaction_size
FROM 
    solana_transactions
GROUP BY 
    token_symbol
ORDER BY 
    avg_transaction_size DESC;
