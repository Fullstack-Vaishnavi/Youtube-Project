# Flight Tracker App

A modern, responsive flight tracking application built with HTML, CSS, and JavaScript. Track real-time flight information, manage favorites, and enjoy a sleek dark/light mode interface.

## Features

- 🛫 Real-time flight tracking
- ⭐ Favorite flights management
- 🌙 Dark/Light mode toggle
- 📱 Responsive design
- 🔍 Flight search functionality
- 📊 Detailed flight information display

## Prerequisites

Before running the application, make sure you have:

- A modern web browser (Chrome, Firefox, Safari, Edge)
- An API key from [Aviation Stack](https://aviationstack.com/)
- A local web server (optional but recommended)

## Setup Instructions

### 1. Get Your API Key

1. Visit [aviationstack.com](https://aviationstack.com/)
2. Sign up for a free account
3. Navigate to your dashboard
4. Copy your API access key

### 2. Configure the API Key

1. Open your `script.js` file
2. Find the API configuration section (usually at the top of the file)
3. Replace `YOUR_API_KEY` with your actual Aviation Stack API key:

```javascript
const API_KEY = 'your_actual_api_key_here';
const BASE_URL = 'http://api.aviationstack.com/v1/flights';
```

### 3. Running the Application

#### Option 1: Simple File Opening
1. Download all project files to a folder
2. Open `index.html` in your web browser
3. **Note:** Some browsers may block API requests when opening files directly due to CORS policies


## Project Structure

```
flight-tracker/
├── index.html          # Main HTML file
├── style.css           # Styling
├── script.js           # Main application logic (contains createFlightCard function)
```

## Key Functions

### Flight Card Creation (script.js)

The core function `createFlightCard` in `script.js` creates comprehensive flight cards that display detailed flight information:

```javascript
function createFlightCard(flight) {
    const flightCard = document.createElement('div');
    flightCard.className = 'flight-card bg-white dark:bg-gray-800 p-6 rounded-2xl shadow-md';
    
    const { departure, arrival, airline, flight: flightInfo, flight_status } = flight;
    const flightIata = flightInfo.iata || flightInfo.number;
    const isFavorited = favorites.includes(flightIata);

    const status = flight_status.replace(/_/g, ' ').replace(/\b\w/g, l => l.toUpperCase());
    const statusColor = {
        'scheduled': 'bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-200',
        'en-route': 'bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-200',
        'landed': 'bg-purple-100 text-purple-800 dark:bg-purple-900 dark:text-purple-200',
        'cancelled': 'bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-200',
        'delayed': 'bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-200'
    }[flight_status] || 'bg-gray-100 text-gray-800 dark:bg-gray-700 dark:text-gray-200';

    const formatTime = (dateString) => dateString ? new Date(dateString).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', hour12: true }) : 'N/A';

    flightCard.innerHTML = `
        <div class="flex justify-between items-start mb-4 border-b border-gray-200 dark:border-gray-700 pb-4">
            <div>
                <p class="text-lg font-bold text-gray-800 dark:text-white">${airline.name || 'N/A'}</p>
                <p class="text-sm text-gray-500 dark:text-gray-400">Flight ${flightIata}</p>
            </div>
            <div class="flex items-center space-x-4">
                <span class="text-sm font-semibold px-3 py-1 rounded-full ${statusColor}">${status}</span>
                <button class="heart-icon ${isFavorited ? 'favorited' : ''}" data-iata="${flightIata}">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 016.364 0L12 7.636l1.318-1.318a4.5 4.5 0 016.364 6.364L12 20.364l-7.682-7.682a4.5 4.5 0 010-6.364z"></path></svg>
                </button>
            </div>
        </div>
        <div class="grid grid-cols-3 items-center text-center my-4">
            <div class="text-left"><p class="text-2xl font-bold">${departure.iata}</p><p class="text-sm text-gray-600 dark:text-gray-300 truncate">${departure.airport || 'N/A'}</p></div>
            <div class="text-gray-400 dark:text-gray-500"><svg class="h-8 w-8 mx-auto" viewBox="0 0 20 20" fill="currentColor"><path d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.428A1 1 0 009.5 16.571V11a1 1 0 112 0v5.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z" /></svg></div>
            <div class="text-right"><p class="text-2xl font-bold">${arrival.iata}</p><p class="text-sm text-gray-600 dark:text-gray-300 truncate">${arrival.airport || 'N/A'}</p></div>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-x-8 gap-y-4 pt-4 border-t border-gray-200 dark:border-gray-700">
            <div class="space-y-2">
                <h4 class="font-semibold text-gray-700 dark:text-gray-200">Departure</h4>
                <p class="text-sm"><strong>Time:</strong> ${formatTime(departure.scheduled)} (Est: ${formatTime(departure.estimated)})</p>
                <p class="text-sm"><strong>Terminal/Gate:</strong> ${departure.terminal || 'N/A'} / ${departure.gate || 'N/A'}</p>
                <p class="text-sm"><strong>Delay:</strong> <span class="${departure.delay ? 'text-red-500 font-semibold' : ''}">${departure.delay ? `${departure.delay} min` : 'No Delay'}</span></p>
            </div>
            <div class="space-y-2">
                <h4 class="font-semibold text-gray-700 dark:text-gray-200">Arrival</h4>
                <p class="text-sm"><strong>Time:</strong> ${formatTime(arrival.scheduled)} (Est: ${formatTime(arrival.estimated)})</p>
                <p class="text-sm"><strong>Terminal/Gate:</strong> ${arrival.terminal || 'N/A'} / ${arrival.gate || 'N/A'}</p>
                <p class="text-sm"><strong>Delay:</strong> <span class="${arrival.delay ? 'text-red-500 font-semibold' : ''}">${arrival.delay ? `${arrival.delay} min` : 'No Delay'}</span></p>
            </div>
        </div>
    `;

    const heartButton = flightCard.querySelector('.heart-icon');
    heartButton.addEventListener('click', (e) => {
        e.stopPropagation();
        toggleFavorite(flightIata, heartButton);
    });
    return flightCard;
}
```

## API Usage

The app uses the Aviation Stack API to fetch flight data. Add this function to your `script.js` file to handle API calls:

```javascript
async function fetchFlights(params = {}) {
    const queryParams = new URLSearchParams({
        access_key: API_KEY,
        ...params
    });
    
    try {
        const response = await fetch(`${BASE_URL}?${queryParams}`);
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error fetching flights:', error);
        return null;
    }
}
```

## Troubleshooting

### Common Issues

1. **API Key Not Working**
   - Verify your API key is correct
   - Check if you've exceeded your API rate limits
   - Ensure you're using the correct API endpoint

2. **CORS Errors**
   - Use a local web server instead of opening files directly
   - Consider using a proxy server for development

3. **Flights Not Loading**
   - Check browser console for error messages
   - Verify your internet connection
   - Ensure the Aviation Stack API is accessible

### API Rate Limits

- Free tier: 1,000 requests per month
- Monitor your usage in the Aviation Stack dashboard
- Consider upgrading for higher limits if needed

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For issues related to:
- **Aviation Stack API**: Visit [aviationstack.com/documentation](https://aviationstack.com/documentation)
- **App functionality**: Create an issue in this repository

---

**Happy flight tracking! ✈️**