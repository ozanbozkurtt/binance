import requests
import time

last_price = None

def get_btcusdt_price():
    url = "https://api.binance.com/api/v3/klines"
    params = {
        "symbol": "BTCUSDT",
        "interval": "5m",
        "limit": 1
    }
    response = requests.get(url, params=params)
    data = response.json()
    if len(data) > 0:
        return float(data[0][4])  # Son kapanış fiyatını al
    else:
        return None

def check_price_change(new_price):
    global last_price
    if last_price is not None:
        if new_price > last_price:
            change_message = f"BTCUSDT exchange rate increased from {last_price} to {new_price}\n"
        elif new_price < last_price:
            change_message = f"BTCUSDT exchange rate decreased from {last_price} to {new_price}\n"
        else:
            change_message = f"BTCUSDT exchange rate stayed the same at {new_price}\n"
        print(change_message)
        with open("exchange_rate_changes.txt", "a") as file:
            file.write(change_message)
    last_price = new_price

def main():
    while True:
        btcusdt_price = get_btcusdt_price()
        if btcusdt_price is not None:
            print(f"BTCUSDT exchange rate: {btcusdt_price}")
            check_price_change(btcusdt_price)
        else:
            print("Failed to fetch exchange rate.")
        
        time.sleep(30)  # 5 dakika bekle

if __name__ == "__main__":
    main()
