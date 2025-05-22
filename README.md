
# Alchemi Faucet

**AlchemiFaucet** is a Python automation tool designed to streamline the process of claiming Sepolia ETH from the [Alchemy Sepolia Faucet](https://www.alchemy.com/faucets/ethereum-sepolia).  
It leverages browser automation to interact with the faucet, making it easy to schedule regular claims for development and testing purposes.

---

## Features

- Automates Sepolia ETH claims from the Alchemy Faucet
- Headless browser operation for efficiency
- Easy to schedule via cronjob or task scheduler
- Written in Python for easy customization

---

## Requirements

- Python 3.7+
- [pyppeteer](https://github.com/pyppeteer/pyppeteer) (for browser automation)

Install dependencies:
```bash
pip install pyppeteer
```

---

## Usage

1. **Clone the repository:**
    ```bash
    git clone https://github.com/AndreiPlazzaSouza/AlchemiFaucet.git
    cd AlchemiFaucet
    ```

2. **Edit the script:**
    - Open the main Python script (e.g., `alchemi_faucet.py`).
    - Replace `'0xYourSepoliaAddressHere'` with your Sepolia wallet address.

3. **Run the script:**
    ```bash
    python alchemi_faucet.py
    ```

---

## Scheduling with Cronjob

To automate claims, add a cronjob entry (Linux/macOS):

```cron
0 1 * * * /usr/bin/python3 /path/to/AlchemiFaucet/alchemi_faucet.py
```
This example runs the script every day at 1:00 AM.

---

## Example Script

```python
import asyncio
from pyppeteer import launch

async def claim_sepolia(wallet_address):
    browser = await launch(headless=True, args=['--no-sandbox'])
    page = await browser.newPage()
    await page.goto('https://www.alchemy.com/faucets/ethereum-sepolia', {'waitUntil': 'networkidle2'})
    await page.waitForSelector('input[type="text"]')
    await page.type('input[type="text"]', wallet_address)
    await page.waitForSelector('button[type="submit"]')
    await page.click('button[type="submit"]')
    await page.waitFor(5000)
    await browser.close()

if __name__ == '__main__':
    wallet_address = '0xYourSepoliaAddressHere'
    asyncio.get_event_loop().run_until_complete(claim_sepolia(wallet_address))
```

---

## Notes

- **Selectors may need adjustment:** If the faucet page changes, update the input and button selectors in the script.
- **CAPTCHA Handling:** The script cannot bypass CAPTCHAs. Manual intervention may be required.
- **Respect faucet rules:** Do not abuse the faucet. Use only for testnet and development purposes.

---

## License

See [LICENSE](LICENSE) for details.

---



---
Answer from Perplexity: https://www.perplexity.ai/search/megaeth-wallet-creator-bulk-wi-FVJ2uP5_QI2VyZkWpFz2aw?utm_source=copy_output
