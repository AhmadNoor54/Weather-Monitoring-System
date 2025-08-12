# 🌤️ Weather Monitoring System

A comprehensive C-based weather monitoring system that fetches real-time weather data from OpenWeatherMap API, processes environmental parameters, and provides automated alerts and reporting capabilities.

## ✨ Features

- **Real-time Weather Data**: Fetches current weather information for any city
- **Multi-parameter Monitoring**: Tracks temperature, humidity, wind speed, and air pressure
- **Automated Alerts**: Configurable threshold-based alerting system
- **Email Notifications**: Automated email reporting with data attachments
- **Continuous Monitoring**: Background script for continuous data collection
- **Data Logging**: Saves raw API responses and processed data to files
- **JSON Processing**: Robust JSON parsing and data extraction

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   OpenWeather   │    │   Weather App   │    │   Email System  │
│      API        │◄──►│   (weather.c)   │◄──►│  (email_sender) │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │
                              ▼
                       ┌─────────────────┐
                       │  Data Files     │
                       │ • raw_data.txt  │
                       │ • process_data  │
                       │ • report.txt    │
                       └─────────────────┘
```

## 📋 Prerequisites

Before running this project, ensure you have the following installed:

### Required Libraries
- **libcurl**: HTTP client library
- **jansson**: JSON parsing library
- **GCC**: C compiler

### Installation Commands

#### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install libcurl4-openssl-dev libjansson-dev gcc make
```

#### CentOS/RHEL/Fedora:
```bash
sudo yum install libcurl-devel jansson-devel gcc make
# or for newer versions:
sudo dnf install libcurl-devel jansson-devel gcc make
```

#### macOS (using Homebrew):
```bash
brew install curl jansson gcc
```

#### Windows (using MSYS2/MinGW):
```bash
pacman -S mingw-w64-x86_64-curl mingw-w64-x86_64-jansson mingw-w64-x86_64-gcc
```

## 🚀 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/weather-monitoring-system.git
   cd weather-monitoring-system
   ```

2. **Compile the project:**
   ```bash
   gcc -o weather weather.c weather_utils.c email_sender.c -lcurl -ljansson
   ```

3. **Configure your API key:**
   - Get a free API key from [OpenWeatherMap](https://openweathermap.org/api)
   - Edit `weather.c` and replace the API key on line 12:
   ```c
   const char *api_key = "YOUR_API_KEY_HERE";
   ```

4. **Configure email settings (optional):**
   - Edit `send_email.sh` to set your email recipient
   - Ensure your system has mail utilities configured

## 📖 Usage

### Basic Usage

Run the weather monitoring application:
```bash
./weather
```

### Continuous Monitoring

Start the monitoring script for continuous data collection:
```bash
chmod +x monitoring_script.sh
./monitoring_script.sh
```

### Manual Email Sending

Send a test email:
```bash
chmod +x send_email.sh
./send_email.sh
```

## 📊 Output Files

The system generates several output files:

- **`raw_data.txt`**: Raw JSON response from the OpenWeatherMap API
- **`process_data.txt`**: Processed environmental data (temperature, humidity, wind speed, pressure)
- **`report.txt`**: Alert reports with timestamp and threshold notifications

### Sample Output

**process_data.txt:**
```
Environmental Data Report
-------------------------
Average Temperature: 28.90°C
Average Humidity: 65.00%
Average Wind Speed: 1.54 m/s
Average Air Pressure: 1010.00 hPa
```

**report.txt:**
```
Environmental Data Report
-------------------------
Report Time: 2024-11-20 19:41:51
Average Temperature: 0.09°C
Alert Message: ALERT: Average temperature low then the threshold value !
```

## ⚙️ Configuration

### Threshold Settings

Edit the threshold value in `weather_utils.h`:
```c
#define THRESHOLD 10.0  // Temperature threshold in Celsius
```

### City Configuration

Change the monitored city in `weather.c`:
```c
strcpy(city, "your_city_name");
```

### Email Configuration

Update email settings in `send_email.sh`:
```bash
recipient="your_email@example.com"
subject="Weather Alert"
message="Weather monitoring alert"
```

## 🔧 Project Structure

```
weather-monitoring-system/
├── weather.c              # Main application file
├── weather_utils.c        # Utility functions for data processing
├── weather_utils.h        # Header file for weather utilities
├── email_sender.c         # Email functionality implementation
├── email_sender.h         # Email sender header
├── monitoring_script.sh   # Continuous monitoring script
├── send_email.sh          # Email sending script
├── raw_data.txt           # Raw API response data
├── process_data.txt       # Processed environmental data
├── report.txt             # Alert reports
└── README.md              # This file
```

## 🛠️ Development

### Adding New Weather Parameters

1. Add new calculation functions in `weather_utils.c`
2. Update the header file `weather_utils.h`
3. Modify the main function in `weather.c` to include new parameters

### Custom Alert Conditions

Modify the `display_alert()` function in `weather_utils.c` to add custom alert conditions based on your requirements.

## 🐛 Troubleshooting

### Common Issues

1. **Compilation Errors:**
   - Ensure all required libraries are installed
   - Check that the library paths are correctly set

2. **API Errors:**
   - Verify your API key is valid and has proper permissions
   - Check your internet connection

3. **Email Not Working:**
   - Ensure mail utilities are properly configured
   - Check SMTP settings if using external email services

### Debug Mode

Add debug output by modifying the code to include more detailed logging:
```c
#ifdef DEBUG
    printf("Debug: API Response: %s\n", data);
#endif
```

## 📝 API Reference

### OpenWeatherMap API

This project uses the OpenWeatherMap Current Weather Data API:
- **Endpoint**: `https://api.openweathermap.org/data/2.5/weather`
- **Parameters**: `q` (city), `appid` (API key), `units` (metric)
- **Response**: JSON format with weather data

### Key Functions

- `get_weather()`: Fetches weather data from API
- `calculate_average_temperature()`: Processes temperature data
- `generate_process_data()`: Creates formatted reports
- `send_email_with_attachment()`: Sends email notifications

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [OpenWeatherMap](https://openweathermap.org/) for providing the weather API
- [libcurl](https://curl.se/libcurl/) for HTTP client functionality
- [jansson](https://github.com/akheron/jansson) for JSON parsing

## 📞 Support

If you encounter any issues or have questions:

1. Check the [Issues](https://github.com/AhmadNoor54/weather-monitoring-system/issues) page
2. Create a new issue with detailed information
3. Contact the maintainers

---

**Made with ❤️ for environmental monitoring and data analysis** 