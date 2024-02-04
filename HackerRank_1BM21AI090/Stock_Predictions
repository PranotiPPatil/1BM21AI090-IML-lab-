class StockTrader:
    def _init_(self):
        self.portfolio = {}

    def make_decision(self, m, k, stocks):
        transactions = []

        for stock in stocks:
            name, owned, prices = stock[0], stock[1], stock[2:]
            current_price = prices[-1]

            action, quantity = self.decide_action(name, owned, current_price, m, prices)

            if action == "BUY":
                transactions.append((name, action, quantity))
                self.portfolio[name] = self.portfolio.get(name, 0) + quantity
                m -= quantity * current_price
            elif action == "SELL":
                transactions.append((name, action, quantity))
                self.portfolio[name] -= quantity
                m += quantity * current_price

        return transactions

    def decide_action(self, name, owned, current_price, m, prices):
        if current_price < min(prices):
            return "BUY", int(m / current_price)
        elif current_price > max(prices):
            return "SELL", owned
        else:
            return "HOLD", 0


def main():
    trader = StockTrader()
    m, k, d = map(int, input().split())
    stocks = [input().split() for _ in range(k)]

    transactions = trader.make_decision(m, k, stocks)

    print(len(transactions))
    for transaction in transactions:
        print(" ".join(map(str, transaction)))


if __name__ == "__main__":
    main()
