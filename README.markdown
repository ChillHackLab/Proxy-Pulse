# ProxyPulse - Proxy Testing Tool

ProxyPulse is a robust command-line tool for testing proxy servers, designed for pentesters, ethical hackers, developers, and network administrators. It verifies proxy functionality, measures latency, and supports HTTP, HTTPS, SOCKS4, and SOCKS5 protocols. Developed by **ChillHack Hong Kong Web Development**, ProxyPulse ensures reliable and efficient proxy testing.

## Features

- **Multi-Protocol Support**: Tests HTTP, HTTPS, SOCKS4, and SOCKS5 proxies.
- **Concurrent Testing**: Uses multi-threading for faster testing (default: 10 threads).
- **Latency Measurement**: Classifies proxies as fast (< 500ms), normal (500ms–1000ms), or slow (> 1000ms) based on a customizable threshold.
- **Retry Mechanism**: Retries failed requests with doubled timeout for reliability.
- **Flexible Output**: Saves working proxies in TXT, JSON, or CSV formats.
- **Progress Tracking**: Displays a progress bar using `tqdm`.
- **Color-Coded Results**: Uses `colorama` for clear, color-coded output (green for fast, cyan for normal, yellow for slow, red for non-working).
- **Custom Test URLs**: Supports default test URLs or a user-specified URL.

## Installation

### Prerequisites
- Python 3.6+
- Required packages:
  ```bash
  pip install requests colorama tqdm
  ```

### Setup
1. Clone or download the repository from [ChillHack](https://chillhack.net).
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Rename the script to `pp.py` (if desired) for shorter command-line usage:
   ```bash
   mv proxypulse.py pp.py
   ```

## Usage

ProxyPulse tests proxies listed in a file, with one proxy per line in formats like:
```
http://192.168.1.1:8080
socks5://user:pass@192.168.1.2:1080
192.168.1.3:3128
```

### Command-Line Arguments
```bash
python pp.py -f proxy_list.txt [options]
```

| Option             | Description                                                                 |
|--------------------|-----------------------------------------------------------------------------|
| `-f`, `--file`     | **Required**. Path to the proxy list file (e.g., `proxy_list.txt`).         |
| `-o`, `--output`   | Path to save working proxies (e.g., `working_proxies.txt`).                 |
| `-t`, `--threshold`| Latency threshold for fast proxies in milliseconds (default: 1000).         |
| `--threads`        | Maximum number of threads for concurrent testing (default: 10).             |
| `--timeout`        | Request timeout in seconds (default: 5). Retries once with double timeout.  |
| `--url`            | Custom test URL (overrides default test URLs).                              |

### Example Commands
- **Basic execution**:
  ```bash
  python pp.py -f proxy_list.txt
  ```
  Tests proxies with default settings (10 threads, 1000ms threshold, 5s timeout).

- **With custom output and threshold**:
  ```bash
  python pp.py -f proxy_list.txt -o working_proxies.txt -t 500
  ```
  Saves working proxies to `working_proxies.txt` with a 500ms threshold.

- **With custom URL and threads**:
  ```bash
  python pp.py -f proxy_list.txt --url https://example.com --threads 20
  ```
  Uses a custom test URL and 20 threads.

### Example Output
```
Progress: 100%|██████████| 3/3 [00:05<00:00,  1.67s/it]
http://192.168.1.1:8080: working, and fast (Speed: 200.50 ms)
socks5://user:pass@192.168.1.2:1080: working, normal speed (Speed: 600.75 ms)
192.168.1.3:3128: not working (Connection failed)
Do you want to save the working proxies to a new file? (y/n):
```

## Example Proxy List File
Create `proxy_list.txt` with:
```
http://192.168.1.1:8080
socks5://user:pass@192.168.1.2:1080
192.168.1.3:3128
```

## Notes
- Ensure the proxy list file exists and is not empty.
- Default test URLs: `https://httpbin.org/ip`, `https://ifconfig.me/ip`, `https://api.ipify.org?format=json`. Override with `--url`.
- Authenticated proxies use the format `protocol://username:password@ip:port`.
- The tool retries failed requests with double the timeout to handle temporary network issues.
- Rename the script to `pp.py` for convenience, as shown in the usage examples.

## Contributing
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature-name`).
3. Commit changes (`git commit -m "Add feature"`).
4. Push to the branch (`git push origin feature-name`).
5. Open a pull request.

Contact **info@chilhack.net** for questions or suggestions.

## License
MIT License. See [LICENSE](LICENSE) for details.

## Contact
- **Developer**: Jake, ChillHack Hong Kong Web Development
- **Email**: [info@chilhack.net](mailto:info@chilhack.net)
- **Website**: [https://chillhack.net](https://chillhack.net)

## Disclaimer
ProxyPulse is for ethical hacking and penetration testing only. Ensure you have permission to test proxies and comply with all applicable laws.