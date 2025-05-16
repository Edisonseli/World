<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>World Countries Learning App</title>
    <style>
        /* Reset and base styles */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f9fafb;
            color: #111827;
            line-height: 1.5;
        }

        /* Background map */
        .background-map {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.15;
            background-image: url('https://hebbkx1anhila5yf.public.blob.vercel-storage.com/placeholder-ObxMt4d3T5MDA2Ca7JyHf5lCNuxMZN.png');
            background-size: cover;
            background-position: center;
        }

        /* Container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem 1rem;
            position: relative;
            z-index: 1;
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 2rem;
        }

        .header h1 {
            font-size: 2.5rem;
            font-weight: 700;
            margin-bottom: 0.5rem;
            color: #111827;
        }

        .header p {
            font-size: 1.25rem;
            color: #6b7280;
        }

        /* Search */
        .search-container {
            position: relative;
            max-width: 500px;
            margin: 0 auto 2rem auto;
        }

        .search-icon {
            position: absolute;
            left: 12px;
            top: 12px;
            color: #6b7280;
        }

        .search-input {
            width: 100%;
            padding: 0.75rem 1rem 0.75rem 2.5rem;
            border: 1px solid #e5e7eb;
            border-radius: 0.375rem;
            font-size: 1rem;
            outline: none;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        .search-input:focus {
            border-color: #2563eb;
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.1);
        }

        /* Main grid */
        .grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1.5rem;
        }

        @media (min-width: 768px) {
            .grid {
                grid-template-columns: 1fr 2fr;
            }
        }

        /* Card */
        .card {
            background-color: white;
            border-radius: 0.5rem;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .card-header {
            padding: 1.25rem 1.5rem;
            border-bottom: 1px solid #f3f4f6;
        }

        .card-title {
            font-size: 1.25rem;
            font-weight: 600;
            color: #111827;
        }

        .card-description {
            font-size: 0.875rem;
            color: #6b7280;
            margin-top: 0.25rem;
        }

        .card-content {
            padding: 1.5rem;
        }

        /* Country list */
        .country-list {
            max-height: 60vh;
            overflow-y: auto;
            scrollbar-width: thin;
            scrollbar-color: #d1d5db #f3f4f6;
        }

        .country-list::-webkit-scrollbar {
            width: 6px;
        }

        .country-list::-webkit-scrollbar-track {
            background: #f3f4f6;
        }

        .country-list::-webkit-scrollbar-thumb {
            background-color: #d1d5db;
            border-radius: 3px;
        }

        .country-button {
            display: block;
            width: 100%;
            text-align: left;
            padding: 0.5rem 0.75rem;
            border: none;
            background-color: transparent;
            border-radius: 0.25rem;
            font-size: 0.875rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .country-button:hover {
            background-color: #f3f4f6;
        }

        .country-button.selected {
            background-color: #2563eb;
            color: white;
        }

        /* Country detail */
        .country-detail-header {
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
            margin-bottom: 1.5rem;
        }

        @media (min-width: 768px) {
            .country-detail-header {
                flex-direction: row;
            }
        }

        .flag-container {
            position: relative;
            width: 100%;
            height: 8rem;
            overflow: hidden;
            border-radius: 0.375rem;
            border: 1px solid #e5e7eb;
            flex-shrink: 0;
        }

        @media (min-width: 768px) {
            .flag-container {
                width: 12rem;
            }
        }

        .flag-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .country-info h2 {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 0.25rem;
        }

        .country-info p {
            color: #6b7280;
            margin-bottom: 0.75rem;
        }

        .country-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.5rem 1rem;
            margin-top: 0.75rem;
        }

        .country-stat {
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .country-stat-icon {
            color: #6b7280;
        }

        /* Tabs */
        .tabs {
            margin-top: 1.5rem;
        }

        .tabs-list {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 0.5rem;
            margin-bottom: 1rem;
        }

        .tab-button {
            padding: 0.5rem;
            background-color: #f3f4f6;
            border: 1px solid #e5e7eb;
            border-radius: 0.25rem;
            font-size: 0.875rem;
            cursor: pointer;
            transition: all 0.2s;
        }

        .tab-button:hover {
            background-color: #e5e7eb;
        }

        .tab-button.active {
            background-color: #2563eb;
            color: white;
            border-color: #2563eb;
        }

        .tab-content {
            display: none;
            padding: 1rem;
            background-color: #f9fafb;
            border-radius: 0.375rem;
        }

        .tab-content.active {
            display: block;
        }

        .tab-content h3 {
            font-size: 1rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .tab-content p {
            margin-bottom: 1rem;
        }

        .tab-content-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 1rem;
        }

        @media (min-width: 768px) {
            .tab-content-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        .tab-content-item h4 {
            font-size: 0.875rem;
            font-weight: 600;
            margin-bottom: 0.25rem;
        }

        .tab-content-item p {
            color: #6b7280;
            font-size: 0.875rem;
        }

        /* Welcome screen */
        .welcome-screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 50vh;
            text-align: center;
            padding: 1rem;
        }

        .globe-image {
            width: 200px;
            height: 200px;
            border-radius: 50%;
            margin-bottom: 1rem;
        }

        .welcome-screen h3 {
            font-size: 1.25rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        .welcome-screen p {
            color: #6b7280;
            margin-bottom: 1rem;
        }

        .random-button {
            padding: 0.5rem 1rem;
            background-color: #2563eb;
            color: white;
            border: none;
            border-radius: 0.25rem;
            font-size: 0.875rem;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .random-button:hover {
            background-color: #1d4ed8;
        }

        /* Loading skeleton */
        .skeleton {
            background-color: #e5e7eb;
            border-radius: 0.25rem;
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0%, 100% {
                opacity: 0.5;
            }
            50% {
                opacity: 1;
            }
        }

        .skeleton-header {
            display: flex;
            gap: 1.5rem;
            margin-bottom: 1.5rem;
        }

        .skeleton-flag {
            width: 12rem;
            height: 8rem;
            border-radius: 0.375rem;
        }

        .skeleton-info {
            flex: 1;
        }

        .skeleton-title {
            height: 2rem;
            width: 12rem;
            margin-bottom: 0.5rem;
        }

        .skeleton-subtitle {
            height: 1rem;
            width: 16rem;
            margin-bottom: 1rem;
        }

        .skeleton-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 0.5rem;
        }

        .skeleton-stat {
            height: 1rem;
            width: 8rem;
        }

        .skeleton-tabs {
            height: 2.5rem;
            margin-bottom: 1rem;
        }

        .skeleton-content {
            height: 8rem;
        }

        /* Map image */
        .map-image-container {
            position: relative;
            width: 100%;
            aspect-ratio: 16/9;
            overflow: hidden;
            border-radius: 0.375rem;
            border: 1px solid #e5e7eb;
            margin-top: 0.5rem;
        }

        .map-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        /* Description section */
        .description-header {
            display: flex;
            align-items: flex-start;
            gap: 0.5rem;
            margin-bottom: 0.75rem;
        }

        .description-icon {
            color: #6b7280;
            flex-shrink: 0;
            margin-top: 0.25rem;
        }
    </style>
</head>
<body>
    <!-- Background Map -->
    <div class="background-map"></div>

    <div class="container">
        <!-- Header -->
        <header class="header">
            <h1>Explore Our World</h1>
            <p>Learn about countries and cultures from around the globe</p>
        </header>

        <!-- Search -->
        <div class="search-container">
            <svg class="search-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="11" cy="11" r="8"></circle>
                <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
            </svg>
            <input type="text" id="search-input" class="search-input" placeholder="Search for a country...">
        </div>

        <!-- Main Grid -->
        <div class="grid">
            <!-- Countries List Card -->
            <div class="card">
                <div class="card-header">
                    <h2 class="card-title">Countries</h2>
                    <p class="card-description">Select a country to learn more</p>
                </div>
                <div class="card-content">
                    <div id="country-list" class="country-list">
                        <!-- Country buttons will be inserted here by JavaScript -->
                    </div>
                </div>
            </div>

            <!-- Country Detail Card -->
            <div class="card">
                <div class="card-header">
                    <h2 id="detail-title" class="card-title">Select a Country</h2>
                    <p id="detail-description" class="card-description">Click on a country from the list to view details</p>
                </div>
                <div class="card-content">
                    <div id="country-detail">
                        <!-- Welcome screen shown initially -->
                        <div id="welcome-screen" class="welcome-screen">
                            <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/placeholder-ObxMt4d3T5MDA2Ca7JyHf5lCNuxMZN.png" alt="Globe Illustration" class="globe-image">
                            <h3>Welcome to the World Countries App</h3>
                            <p>Select a country from the list to discover fascinating facts and information</p>
                            <button id="random-country-button" class="random-button">Explore Random Country</button>
                        </div>

                        <!-- Country detail will be inserted here by JavaScript -->
                        <div id="country-info" style="display: none;">
                            <!-- Loading skeleton -->
                            <div id="loading-skeleton" style="display: none;">
                                <div class="skeleton-header">
                                    <div class="skeleton skeleton-flag"></div>
                                    <div class="skeleton-info">
                                        <div class="skeleton skeleton-title"></div>
                                        <div class="skeleton skeleton-subtitle"></div>
                                        <div class="skeleton-stats">
                                            <div class="skeleton skeleton-stat"></div>
                                            <div class="skeleton skeleton-stat"></div>
                                            <div class="skeleton skeleton-stat"></div>
                                            <div class="skeleton skeleton-stat"></div>
                                        </div>
                                    </div>
                                </div>
                                <div class="skeleton skeleton-tabs"></div>
                                <div class="skeleton skeleton-content"></div>
                            </div>

                            <!-- Country detail content -->
                            <div id="country-detail-content" style="display: none;">
                                <!-- Will be populated by JavaScript -->
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Country data
        const countries = [
            "Afghanistan", "Albania", "Algeria", "Andorra", "Angola", "Antigua and Barbuda", "Argentina", "Armenia", 
            "Australia", "Austria", "Azerbaijan", "Bahamas", "Bahrain", "Bangladesh", "Barbados", "Belarus", "Belgium", 
            "Belize", "Benin", "Bhutan", "Bolivia", "Bosnia and Herzegovina", "Botswana", "Brazil", "Brunei", "Bulgaria", 
            "Burkina Faso", "Burundi", "Cabo Verde", "Cambodia", "Cameroon", "Canada", "Central African Republic", "Chad", 
            "Chile", "China", "Colombia", "Comoros", "Congo", "Costa Rica", "Croatia", "Cuba", "Cyprus", "Czechia", 
            "Denmark", "Djibouti", "Dominica", "Dominican Republic", "Timor-Leste", "Ecuador", "Egypt", "El Salvador", 
            "Equatorial Guinea", "Eritrea", "Estonia", "Eswatini", "Ethiopia", "Fiji", "Finland", "France", "Gabon", 
            "Gambia", "Georgia", "Germany", "Ghana", "Greece", "Grenada", "Guatemala", "Guinea", "Guinea-Bissau", "Guyana", 
            "Haiti", "Honduras", "Hungary", "Iceland", "India", "Indonesia", "Iran", "Iraq", "Ireland", "Israel", "Italy", 
            "Jamaica", "Japan", "Jordan", "Kazakhstan", "Kenya", "Kiribati", "North Korea", "South Korea", "Kosovo", 
            "Kuwait", "Kyrgyzstan", "Laos", "Latvia", "Lebanon", "Lesotho", "Liberia", "Libya", "Liechtenstein", 
            "Lithuania", "Luxembourg", "Madagascar", "Malawi", "Malaysia", "Maldives", "Mali", "Malta", "Marshall Islands", 
            "Mauritania", "Mauritius", "Mexico", "Micronesia", "Moldova", "Monaco", "Mongolia", "Montenegro", "Morocco", 
            "Mozambique", "Myanmar", "Namibia", "Nauru", "Nepal", "Netherlands", "New Zealand", "Nicaragua", "Niger", 
            "Nigeria", "North Macedonia", "Norway", "Oman", "Pakistan", "Palau", "Palestine", "Panama", "Papua New Guinea", 
            "Paraguay", "Peru", "Philippines", "Poland", "Portugal", "Qatar", "Romania", "Russia", "Rwanda", 
            "Saint Kitts and Nevis", "Saint Lucia", "Saint Vincent and the Grenadines", "Samoa", "San Marino", 
            "Sao Tome and Principe", "Saudi Arabia", "Senegal", "Serbia", "Seychelles", "Sierra Leone", "Singapore", 
            "Slovakia", "Slovenia", "Solomon Islands", "Somalia", "South Africa", "South Sudan", "Spain", "Sri Lanka", 
            "Sudan", "Suriname", "Sweden", "Switzerland", "Syria", "Taiwan", "Tajikistan", "Tanzania", "Thailand", "Togo", 
            "Tonga", "Trinidad and Tobago", "Tunisia", "Turkey", "Turkmenistan", "Tuvalu", "Uganda", "Ukraine", 
            "United Arab Emirates", "United Kingdom", "United States", "Uruguay", "Uzbekistan", "Vanuatu", "Vatican City", 
            "Venezuela", "Vietnam", "Yemen", "Zambia", "Zimbabwe"
        ];

        // Cache for country descriptions
        let countryDescriptionsCache = null;

        // DOM elements
        const countryListElement = document.getElementById('country-list');
        const searchInput = document.getElementById('search-input');
        const detailTitle = document.getElementById('detail-title');
        const detailDescription = document.getElementById('detail-description');
        const welcomeScreen = document.getElementById('welcome-screen');
        const countryInfo = document.getElementById('country-info');
        const loadingSkeleton = document.getElementById('loading-skeleton');
        const countryDetailContent = document.getElementById('country-detail-content');
        const randomCountryButton = document.getElementById('random-country-button');

        // Initialize the app
        function initApp() {
            renderCountryList(countries);
            setupEventListeners();
            fetchCountryDescriptions();
        }

        // Render the list of countries
        function renderCountryList(countriesToRender) {
            countryListElement.innerHTML = '';
            
            if (countriesToRender.length === 0) {
                const noResults = document.createElement('p');
                noResults.textContent = 'No countries found';
                noResults.style.textAlign = 'center';
                noResults.style.padding = '1rem';
                noResults.style.color = '#6b7280';
                countryListElement.appendChild(noResults);
                return;
            }

            countriesToRender.forEach(country => {
                const button = document.createElement('button');
                button.textContent = country;
                button.className = 'country-button';
                button.dataset.country = country;
                countryListElement.appendChild(button);
            });
        }

        // Setup event listeners
        function setupEventListeners() {
            // Country selection
            countryListElement.addEventListener('click', (e) => {
                if (e.target.classList.contains('country-button')) {
                    const country = e.target.dataset.country;
                    selectCountry(country);
                }
            });

            // Search functionality
            searchInput.addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase();
                const filteredCountries = countries.filter(country => 
                    country.toLowerCase().includes(query)
                );
                renderCountryList(filteredCountries);
            });

            // Random country button
            randomCountryButton.addEventListener('click', () => {
                const randomCountry = countries[Math.floor(Math.random() * countries.length)];
                selectCountry(randomCountry);
            });
        }

        // Select a country
        function selectCountry(countryName) {
            // Update UI
            detailTitle.textContent = countryName;
            detailDescription.textContent = 'Learn about this country\'s geography, culture, and more';
            
            // Update selected state in list
            const buttons = countryListElement.querySelectorAll('.country-button');
            buttons.forEach(button => {
                if (button.dataset.country === countryName) {
                    button.classList.add('selected');
                } else {
                    button.classList.remove('selected');
                }
            });

            // Show country info and hide welcome screen
            welcomeScreen.style.display = 'none';
            countryInfo.style.display = 'block';
            loadingSkeleton.style.display = 'block';
            countryDetailContent.style.display = 'none';

            // Fetch country data
            fetchCountryData(countryName);
        }

        // Fetch country data from REST Countries API
        async function fetchCountryData(countryName) {
            try {
                const response = await fetch(`https://restcountries.com/v3.1/name/${countryName}?fullText=true`);
                
                if (!response.ok) {
                    throw new Error('Country information not found');
                }
                
                const data = await response.json();
                renderCountryDetail(data[0], countryName);
            } catch (error) {
                console.error('Error fetching country data:', error);
                renderErrorMessage('Could not load country information. Please try again later.');
            }
        }

        // Fetch country descriptions from CSV
        async function fetchCountryDescriptions() {
            if (countryDescriptionsCache) {
                return countryDescriptionsCache;
            }

            try {
                const response = await fetch('https://hebbkx1anhila5yf.public.blob.vercel-storage.com/all_countries_with_descriptions-uMjNfeAzJ8OiQv0WKhqkR43mDTfzvG.csv');
                
                if (!response.ok) {
                    throw new Error('Failed to fetch country descriptions');
                }
                
                const csvText = await response.text();
                const descriptions = parseCSV(csvText);
                
                countryDescriptionsCache = descriptions;
                return descriptions;
            } catch (error) {
                console.error('Error fetching country descriptions:', error);
                return [];
            }
        }

        // Parse CSV data
        function parseCSV(csvText) {
            const lines = csvText.split('\n');
            const descriptions = [];

            for (let i = 1; i < lines.length; i++) {
                const line = lines[i].trim();
                if (!line) continue;

                // Handle potential commas within the description (which is enclosed in quotes)
                let country = '';
                let description = '';

                // Simple CSV parsing that handles quoted fields
                if (line.startsWith('"')) {
                    // Country name is quoted
                    const firstQuoteEnd = line.indexOf('"', 1);
                    country = line.substring(1, firstQuoteEnd);

                    // Find the start of the description (after the comma)
                    const descStart = line.indexOf(',', firstQuoteEnd) + 1;

                    if (line.charAt(descStart) === '"') {
                        // Description is quoted
                        description = line.substring(descStart + 1, line.lastIndexOf('"'));
                    } else {
                        // Description is not quoted
                        description = line.substring(descStart);
                    }
                } else {
                    // Country name is not quoted
                    const commaIndex = line.indexOf(',');
                    country = line.substring(0, commaIndex);

                    if (line.charAt(commaIndex + 1) === '"') {
                        // Description is quoted
                        description = line.substring(commaIndex + 2, line.lastIndexOf('"'));
                    } else {
                        // Description is not quoted
                        description = line.substring(commaIndex + 1);
                    }
                }

                descriptions.push({
                    Country: country.trim(),
                    Description: description.trim()
                });
            }

            return descriptions;
        }

        // Get country description
        function getCountryDescription(countryName, descriptions) {
            // Try to find an exact match
            const exactMatch = descriptions.find(desc => 
                desc.Country.toLowerCase() === countryName.toLowerCase()
            );

            if (exactMatch) {
                return exactMatch.Description;
            }

            // Try to find a partial match
            const partialMatch = descriptions.find(desc => 
                countryName.toLowerCase().includes(desc.Country.toLowerCase()) || 
                desc.Country.toLowerCase().includes(countryName.toLowerCase())
            );

            if (partialMatch) {
                return partialMatch.Description;
            }

            // Return a default description if no match is found
            return `${countryName} is a country with its own unique culture, history, and geographical features.`;
        }

        // Render country detail
        async function renderCountryDetail(countryData, countryName) {
            // Format numbers
            const formatNumber = (num) => {
                return new Intl.NumberFormat().format(num);
            };

            // Get languages and currencies
            const languages = countryData.languages 
                ? Object.values(countryData.languages).join(', ') 
                : 'Information not available';

            const currencies = countryData.currencies 
                ? Object.values(countryData.currencies).map(c => `${c.name} (${c.symbol})`).join(', ') 
                : 'Information not available';

            // Get country description
            const descriptions = await fetchCountryDescriptions();
            const countryDescription = getCountryDescription(countryName, descriptions);

            // Create HTML for country detail
            const html = `
                <div class="country-detail-header">
                    <div class="flag-container">
                        <img src="${countryData.flags.png}" alt="Flag of ${countryData.name.common}" class="flag-image">
                    </div>
                    <div class="country-info">
                        <h2>${countryData.name.common}</h2>
                        <p>${countryData.name.official}</p>
                        <div class="country-stats">
                            <div class="country-stat">
                                <svg class="country-stat-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"></path>
                                    <circle cx="12" cy="10" r="3"></circle>
                                </svg>
                                <span>Region: ${countryData.region}</span>
                            </div>
                            <div class="country-stat">
                                <svg class="country-stat-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <rect width="16" height="16" x="4" y="4" rx="2"></rect>
                                    <path d="M4 12h16"></path>
                                    <path d="M12 4v16"></path>
                                </svg>
                                <span>Capital: ${countryData.capital?.[0] || 'N/A'}</span>
                            </div>
                            <div class="country-stat">
                                <svg class="country-stat-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"></path>
                                    <circle cx="9" cy="7" r="4"></circle>
                                    <path d="M22 21v-2a4 4 0 0 0-3-3.87"></path>
                                    <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
                                </svg>
                                <span>Population: ${formatNumber(countryData.population)}</span>
                            </div>
                            <div class="country-stat">
                                <svg class="country-stat-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                    <circle cx="12" cy="12" r="10"></circle>
                                    <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path>
                                    <path d="M2 12h20"></path>
                                </svg>
                                <span>Area: ${formatNumber(countryData.area)} km²</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="tabs">
                    <div class="tabs-list">
                        <button class="tab-button active" data-tab="overview">Overview</button>
                        <button class="tab-button" data-tab="description">Description</button>
                        <button class="tab-button" data-tab="culture">Culture</button>
                        <button class="tab-button" data-tab="geography">Geography</button>
                    </div>

                    <div id="overview-tab" class="tab-content active">
                        <h3>About ${countryData.name.common}</h3>
                        <p>
                            ${countryData.name.common} is a country located in ${countryData.subregion || countryData.region}. 
                            Its capital city is ${countryData.capital?.[0] || 'not specified'} and it has a population of ${formatNumber(countryData.population)} people.
                        </p>
                        <div class="tab-content-grid">
                            <div class="tab-content-item">
                                <h4>Languages</h4>
                                <p>${languages}</p>
                            </div>
                            <div class="tab-content-item">
                                <h4>Currencies</h4>
                                <p>${currencies}</p>
                            </div>
                        </div>
                    </div>

                    <div id="description-tab" class="tab-content">
                        <div class="description-header">
                            <svg class="description-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                                <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"></path>
                                <path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"></path>
                            </svg>
                            <h3>Country Description</h3>
                        </div>
                        <p>${countryDescription}</p>
                    </div>

                    <div id="culture-tab" class="tab-content">
                        <h3>Culture of ${countryData.name.common}</h3>
                        <p>
                            ${countryData.name.common} has a rich cultural heritage reflected in its language(s): ${languages}.
                            The country's unique identity is shaped by its history, traditions, and diverse population of ${formatNumber(countryData.population)} people.
                        </p>
                        <div class="tab-content-item" style="margin-top: 1rem;">
                            <h4>Did you know?</h4>
                            <p>
                                Select different countries to learn interesting facts and cultural information about each nation.
                            </p>
                        </div>
                    </div>

                    <div id="geography-tab" class="tab-content">
                        <h3>Geography of ${countryData.name.common}</h3>
                        <p>
                            ${countryData.name.common} is located in ${countryData.region}, specifically in the ${countryData.subregion || 'region'}.
                            It covers an area of ${formatNumber(countryData.area)} square kilometers.
                        </p>
                        <div class="tab-content-item" style="margin-top: 1rem;">
                            <h4>Location</h4>
                            <div class="map-image-container">
                                <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/placeholder-ObxMt4d3T5MDA2Ca7JyHf5lCNuxMZN.png" alt="Map of ${countryData.name.common}" class="map-image">
                            </div>
                        </div>
                    </div>
                </div>
            `;

            // Update the UI
            countryDetailContent.innerHTML = html;
            loadingSkeleton.style.display = 'none';
            countryDetailContent.style.display = 'block';

            // Setup tab functionality
            setupTabs();
        }

        // Setup tabs
        function setupTabs() {
            const tabButtons = document.querySelectorAll('.tab-button');
            const tabContents = document.querySelectorAll('.tab-content');

            tabButtons.forEach(button => {
                button.addEventListener('click', () => {
                    const tabName = button.dataset.tab;
                    
                    // Update active tab button
                    tabButtons.forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                    
                    // Update active tab content
                    tabContents.forEach(content => content.classList.remove('active'));
                    document.getElementById(`${tabName}-tab`).classList.add('active');
                });
            });
        }

        // Render error message
        function renderErrorMessage(message) {
            countryDetailContent.innerHTML = `
                <div style="text-align: center; padding: 2rem;">
                    <p style="color: #ef4444; margin-bottom: 0.5rem;">${message}</p>
                    <p>Try selecting a different country or check your internet connection.</p>
                </div>
            `;
            
            loadingSkeleton.style.display = 'none';
            countryDetailContent.style.display = 'block';
        }

        // Initialize the app when the page loads
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
